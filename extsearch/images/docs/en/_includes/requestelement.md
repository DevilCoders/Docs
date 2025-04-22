## The request element {#requestelement}

The `request` element contains summarized information about the query.

Tags for the `request` element are shown in the table below.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `query` | Query text. | No attributes. ||
|| `page` | The page number in search results. | 
- `first` —The number of the first image on the search results page.
- `last` — The number of the last image on the search results page. ||
|| `sortby` | Parameters for sorting search results. By default, results are sorted by relevance (the “rlv” value). | 
- `order` — Sorting order. The only value used is “descending”.
- `priority` — The priority of some search results over others. The only value used is “no”. ||
|| `maxpassages` | The number of text snippets to generate for each image. | No attributes. || 
|#

> The `groupings` tag. Contains parameters for grouping. No attributes.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `groupby` {#requestgroupby} | Grouping parameters. | 	
- `attr` — Types of sources used. Must have the value “ii”.
- `mode` — Type of grouping.
- `groups-on-page` — Number of search results that can be displayed on a single page.
- `docs-in-group` — Number of images in a group. Must have the value “1”
- `curcateg` — Service attribute. Must have the value “-1”. ||
|#

> The following example shows the `request` element returned for the HTTP request `http://xmlsearch.yandex.com/xmlsearch?text=MarioAndretti&type=pictures&g=1.ii.20.1.-1`
> 
> ```xml
> <request>
>    <query>MarioAndretti</query>
>    <page>0</page>
>    <sortby order="descending" priority="no">rlv</sortby>
>    <maxpassages>2</maxpassages>
>    <groupings>
>       <groupby attr="ii" mode="deep" groups-on-page="20" docs-in-group="1" curcateg="-1"/>
>    </groupings>
> </request>
> ```
