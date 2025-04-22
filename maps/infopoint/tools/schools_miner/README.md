# Infopoint schools road events miner
This program searches for all crosswalks near schools and writes them in output table. For generating suitable xml that can be used for infopoint legacy import see [`school_road_events_xml_generator`](https://a.yandex-team.ru/arc_vcs/maps/infopoint/tools/school_road_events_xml_generator).
## Pipeline
### School organizations extraction (using yql)
Miner utilizes Yandex.Spravochnik's [YT database](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/snapshot) (specifically, [`company`](https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/snapshot/company) table) for searching all relevant schools. Schools are extracted to intermediate table `company` in working directory.
### Schools territory extraction (using yql)
Miner extracts geometries of all ymapsdf [`features`](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft.html) that have type (`ft_type_id` column) of 171 (territory of educational organization) and whether having no parent (`p_ft_id`) or parent of type 168 (schools). Geometries are extracted to intermediate table `territory_geometry` in working directory.
### Crosswalk and road intersection extraction (using yql)
Miner extracts positions of all ymapsdf [junctions](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/jc.html) that are connecting on the same z level [road elements](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/road_el.html) of pedestrain crosswalks and of road for automotives. Found junctions are extracted to intermediate table `crosswalk` in working directory.
### Traffic light extraction (using yql)
Miner extracts positions of all ymapsdf junctions having traffic light [condition](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/road_cond.html) on them. Found junctions are extracted to intermediate table `traffic_light` in working directory.
### Matching school organizations with school territories
Miner builds spatial index of extracted school territories and for every extracted school organiztion searches for territory containing (overlapping) address position of this organization. Thus, every school whether has attached territory or not, in which case it's implied that it has circular territory of some constant radius.
'Spravochnik's organization'<->'ymapsdf territory' matching can be also done using ymapsdf 'feature'<->'parent feature' linkage mechanism, in which case school feature is parent of its territory and 'school feature'<->'Spravochnik's organization' are linked via [`ft_source` ymapsdf table](https://doc.yandex-team.ru/ymaps/ymapsdf/ymapsdf-ref/concepts/ft_source.html). But 'feature'<->'parent feature' link is not always established (as of summer of 2019 only 75% of school territories have parent specified). It's possible, that `ft_source` doesn't always maps ymapsdf feature to Spravochnik's organization either (this is unchecked). Thus, geometrical inclusion is considered to be more reliable 'organization'<->'territory' matcher. At the same time, in rare cases, Spravochnik's organization's address position is set outside corresponding school territory in which case also no matching occurs. Probably, better result can be achieved if both geometrical inclusion and parent with `ft_source` are utilized.
Companies with matched territories are written to intermediate table `company_with_territory` in working directory for debugging/visualization.
### Building traffic light spatial index
Miner builds spatial index of all extracted traffic lights. It then used for checking whether given crosswalk is regulated by traffic light. At the moment, crosswalk is considered to be regulated if it's geometrical distance to traffic light is less than some constant value.
### Searching for crosswalks near school territories
School territories spatial index is build once again. But this time only for territories with matched school organizations and for every organization with no matched territory circular territory of some constant radius is used. For every crosswalk that is not regulated by traffic light closest school territories are found, and, if distance from crosswalk to these territory is less than some predefined constant value, than it's checked whether it's reachable on foot.
For checking reachability on foot pedestrian graph is used. Points with equal interval between them (around 10-20 meters) are distributed over exterior of school territory expanded by some buffer radius (this is done so all the fences fall inside territory). For every such point pedestrian route to crosswalk is build. If there any point with route length less than some predifined value, then this crosswalk is considered to be reachable on foot.
If for given crosswalk not regulated by traffic light there is school territory nearby that is reachable on foot then this crosswalk is placed in resulting road events list.
### Attaching crosswalks to crosswalk groups
In some scenarios, there are multiple crosswalks residing very close to each other around same crossroad (or same road, but different roadways separated by central reservation) and part of these crosswalks are barely close to some school territory while others are barely outside closeness radius. All crosswalks not regulated by traffic lights that are not added to resulting list of road events but close to croswalks that are added, are also added to list, thus if any crosswalk near some crossroad is added to list, all other
crosswalks near same crossroad are also guaranteed to be added.
### Saving result
Resulting list of road events is written to `road_event` table in working dir. Output columns are `lon`, `lat`, `permalink` and `trait`. `trait` column is a string describing road event traits, can be used for further events filtration and can be one of:
* `"regular"` - no special traits;
* `"attached_to_crosswalk_group"` - if crosswalk wasn't initially added to resulting list, but was later attached to crosswalk group;
* `"regulated_by_traffic_light"` - crosswalk is regulated by traffic light;
* `"too_far_on_foot"` - crosswalk is close enough to school territory, but too far on foot (e.g. on the other of some obstacle, like river).
## Config
All configuration is done with config file, example can be found in `conf` dir.<br />
`{`<br />
`"rubricTablePath": "//home/sprav/altay/prod/snapshot/rubric",`<br />
`"companyTablePath": "//home/sprav/altay/prod/snapshot/company",`<br />
Working YT directory, all intermediate and result tables reside in working dir. All existing tables are overriden. If working dir is not specified (missing, don't leave it empty) then temporary directory is created.<br />
`"workingDir": "//home/some_path/schools_miner",`<br />
Whitelist of rubrics, if organization in any rubric that is not in whitelist then it's skipped.<br />
`"rubrics": [30692, 30694, 30723, 31663],`<br />
List of YT directories containing map info in ymapsdf format.<br />
`"ymapsdfDirs": [ "//home/maps/core/garden/stable/ymapsdf/latest/cis1" ],`<br />
`"pedestrianGraphConfigPath": "/some_path/config.xml",`<br />
`"constants": {`<br />
Buffer radius used to expand school territory when checking for reachability on foot. Bigger radius ensures that fences fall inside expanded territory, but can have unwanted side effects, like including unwanted obstacles (like other buildings or small rivers) in expanded territory, so it will be ignored while checking for reachability.<br />
`"territoryBufferRadius": 5,`<br />
Radius of circular territory implied if school has no matched territory from ymapsdf.<br />
`    "defaultTerritoryRadius": 25,`<br />
Crosswalk can be only associated with school if it resides closer than this distance to school's territory (except for crosswalks attached to crosswalk groups).<br />
`    "maxCrosswalkDistanceToTerritory": 75,`<br />
Crosswalk can be only associated with school if there is pedestrian route from school's territory to this crosswalk shorter than this distance (except for crosswalks attached to crosswalk groups). Thus, for example, crosswalks are not attached to the school on the other side of a river if there is no bridge nearby.<br />
`    "maxCrosswalkWalkingDistanceToTerritory": 120,`<br />
Crosswalks that reside closer to each other than this radius are considered to be in the same crosswalk group.<br />
`    "crosswalkGroupAttachmentRadius": 30,`<br />
Crosswalks that reside closer to traffic light than this radius are considered to be regulated by traffic light.<br />
`    "trafficLightRegulationRadius": 25,`<br />
All roads with category less than this are ignored (only for automotive).<br />
`    "minRoadCategory": 1,`<br />
All roads with category greater than this are ignored (only for automotive). For example, unpaved roads have category 9 and are ignored.<br />
`    "maxRoadCategory": 7`<br />
`    }`<br />
`}`<br />
## CLI
Usage:<br />
`schools_miner [OPTIONS] CONFIG_PATH`<br />
OPTIONS:<br />
`-s, --skip-intermediate-tables` - whether should skip updating companies/geometries tables (default: 1)<br />
Example:<br />
`schools_miner -s 0 ~/schools_miner.config`<br />
## easyview
Output tables in working dir `company_with_territory` and `road_events` are compatible with `maps/tools/easyview` input format (see `easyview` documentation). Usage example:
`{ yt --proxy=hahn read-table --format '<format=text>yson' '//SOME_WORKING_DIR/road_event' && yt --proxy=hahn read-table --format '<format=text>yson' '//SOME_WORKING_DIR/schools_with_territories'; } | ./easyview`
## Remarks
In source code all entities storing values in mercator projection units have suffix `Mercator`, eg. `distanceMercator`. Geo coordinates and metric units are assumed otherwise.
