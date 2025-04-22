# Отказ от конфига TARIFF_CATEGORIES_VISIBILITY

## Для чего

На текущий момент размер 
[данного конфига](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/TARIFF_CATEGORIES_VISIBILITY?name=VISIBILIT)
составляет ~15к строк, 
при таком размере существует риск допущения различного рода ошибок, 
которые потенциально могут привести к нежелательным последствиям. 
В более благоприятном случае будет наблюдаться видмость тарифов, 
для которых она не предполагалась. В менее благоприятном случае 
может случиться полная потеря видимости всех тарифов. 

Также в конфиге много неактуальных записей - многие категории
которые есть в конфиге отсутсвуют в tariff_settings. Вот пример: 
`moscow: {'mkk_antifraud', 'universal', 'promo'}`  Т.е в конфиге для 
зоны `moscow` есть настройки для категориий`{'mkk_antifraud', 'universal', 'promo'}`, 
но в tariff_settings этих категориий нет для зоны `moscow`.

<details>
  <summary>Полный список</summary>

```
abakan {'lavka', 'scooters', 'eda', 'drive', 'business2', 'mkk_antifraud'}
abidjan {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
abinsk {'scooters', 'eda', 'lavka'}
accra {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
adler {'scooters', 'drive', 'lavka', 'promo'}
adygejsk {'scooters', 'eda', 'lavka'}
akademgorod {'scooters', 'drive', 'cargocorp', 'lavka'}
aktau {'eda'}
aktobe {'eda'}
alapaevsk {'scooters', 'eda', 'suv', 'lavka'}
alatyr {'scooters', 'eda', 'lavka'}
aleksin {'scooters', 'eda', 'lavka'}
almaty {'scooters', 'lavka', 'drive'}
almetevsk {'scooters', 'lavka'}
altajskij_region {'eda'}
amur_region {'eda'}
anapa {'scooters', 'lavka'}
anapa_airport set()
andijan {'eda', 'econom'}
andreevka {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
angarsk {'scooters', 'eda', 'lavka'}
ann_arbor {'cargocorp', 'econom', 'lavka', 'scooters', 'eda'}
anzherosudzhensk {'scooters', 'eda', 'lavka'}
aprelevka {'scooters', 'cargocorp', 'drive', 'promo'}
ararat_region {'eda'}
arkhangelsk {'cargocorp', 'lavka', 'scooters', 'night', 'eda', 'drive'}
armavir {'scooters', 'lavka'}
armavir_region {'eda'}
arsenev {'scooters', 'eda', 'lavka'}
arsk {'scooters', 'eda', 'lavka'}
artem {'scooters', 'eda', 'lavka'}
arzamas {'scooters', 'eda', 'lavka'}
asbest {'scooters', 'eda', 'lavka'}
asha {'scooters', 'eda', 'lavka'}
astana {'scooters', 'lavka', 'drive'}
astrakhan {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
astrakhan_region {'eda'}
atyrau {'eda'}
avsyunino {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
azov {'scooters', 'eda', 'lavka'}
baden_baden {'scooters', 'comfort', 'eda', 'vip'}
baksan {'scooters', 'eda', 'lavka'}
baku {'eda', 'lavka', 'econom'}
balabanovo {'eda'}
balakhna {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
balakovo {'scooters', 'lavka'}
balashiha {'scooters', 'drive', 'promo'}
balashikha_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
balashov {'scooters', 'eda', 'lavka'}
baltiysk {'scooters', 'eda', 'lavka'}
baranavichy {'eda'}
barnaul {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
bashkortostan_region {'eda'}
bataysk {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
batumi {'eda'}
belaya_glina {'scooters', 'eda', 'lavka'}
belaya_kalitva {'scooters', 'eda', 'lavka'}
belebey {'scooters', 'eda', 'lavka'}
belgorod {'cargocorp', 'lavka', 'scooters', 'night', 'drive'}
belgrade {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
belogorsk {'scooters', 'eda', 'lavka'}
belokurikha {'scooters', 'eda', 'lavka'}
beloozyorskij {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
belorechensk {'scooters', 'eda', 'lavka'}
beloretsk {'scooters', 'eda', 'lavka'}
beltsi {'eda'}
berdsk {'scooters', 'eda', 'lavka'}
bereza {'eda'}
berezniki {'scooters', 'eda', 'lavka'}
bergen {'eda'}
berlin {'scooters', 'comfort', 'eda'}
birobidgan {'scooters', 'eda', 'lavka'}
birsk {'scooters', 'eda', 'lavka'}
bishkek {'eda'}
biysk {'scooters', 'eda', 'lavka'}
blagoveschensk_bashkortostan {'eda'}
blagoveshchensk {'scooters', 'lavka'}
bobruisk {'eda'}
bologoe {'scooters', 'eda', 'lavka'}
bolshie_vyazyomy {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
bolshoy_kamen {'scooters', 'eda', 'lavka'}
bor {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
borisoglebsk {'scooters', 'eda', 'lavka'}
borisov {'eda'}
borovichy {'scooters', 'eda', 'lavka'}
boryasvo {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
bouake {'eda'}
bratsk {'scooters', 'eda', 'lavka'}
brest {'lavka'}
brest_region {'eda'}
bronnitsi {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
bryansk {'scooters', 'lavka', 'promo'}
bryansk_region {'eda'}
bryuhoveckaya {'scooters', 'eda', 'lavka'}
bucharest {'cargocorp', 'econom', 'minivan', 'lavka', 'vip', 'scooters', 'ultimate', 'eda', 'drive', 'business', 'comfortplus'}
budyonnovsk {'scooters', 'eda', 'lavka'}
bugulma {'scooters', 'eda', 'lavka'}
buguruslan {'scooters', 'eda', 'lavka'}
buinsk {'scooters', 'eda', 'lavka'}
buynaksk {'scooters', 'eda', 'lavka'}
buzuluk {'scooters', 'eda', 'lavka'}
bykovo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
cape_town {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
chaikovsky {'scooters', 'eda', 'lavka'}
chapaevsk {'eda'}
chebarkul {'eda'}
cheboksary {'cargocorp', 'lavka', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
chechnya_region {'eda'}
chegem {'scooters', 'eda', 'lavka'}
chehov {'scooters', 'cargocorp', 'drive', 'promo'}
chelyabinsk {'cargocorp', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
chelyabinsk_region {'eda'}
cherepovets {'scooters', 'lavka'}
cherkessk {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
chernogolovka {'scooters', 'cargocorp', 'drive', 'promo'}
chernogorsk {'scooters', 'eda', 'lavka'}
chernyahovsk {'scooters', 'eda', 'lavka'}
chimkent {'eda'}
chishmy {'vezeteconom', 'eda'}
chistopol {'scooters', 'eda', 'lavka'}
chita {'scooters', 'eda', 'lavka'}
chusovoy {'scooters', 'eda', 'lavka'}
chuvashiya_region {'eda'}
dagomis set()
dakar {'eda', 'business'}
daugavpils {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
dedovsk {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
derbent {'scooters', 'eda', 'lavka'}
dimitrovgrad {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
dinskaya {'scooters', 'eda', 'lavka'}
dme {'scooters', 'cargocorp', 'courier', 'promo'}
dmitrov {'scooters', 'cargocorp', 'drive', 'promo'}
dnipro {'eda'}
dobryanka {'scooters', 'eda', 'lavka'}
dolgoderevenskoye {'eda'}
dolgoprudniy {'scooters', 'drive', 'promo'}
dolgoprudniy_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
domodedovo {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
domodedovo_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
douala {'eda'}
drezna {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
dubna {'scooters', 'cargocorp', 'drive', 'promo'}
dyurtyuli {'scooters', 'eda', 'lavka'}
dzerzhinsk {'scooters', 'cargocorp', 'lavka', 'drive'}
dzerzhinsk_minsk {'eda'}
dzerzhinsky {'scooters', 'drive', 'promo'}
dzerzhinsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
egorievsk {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
ehkspoforum {'vezeteconom', 'eda'}
ekb {'scooters', 'mkk_antifraud', 'drive', 'promo'}
ekibastuz {'eda'}
elabuga {'scooters', 'eda', 'lavka'}
electrostal {'scooters', 'cargocorp', 'drive', 'promo'}
elektrogorsk {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
elektrougli {'scooters', 'cargocorp', 'drive', 'promo'}
elista {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
engels {'scooters', 'lavka', 'promo'}
ershov {'scooters', 'eda', 'lavka'}
essentuky {'scooters', 'lavka'}
fergana {'eda', 'econom'}
fryazino {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
fryazino_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
gagarin {'scooters', 'eda', 'lavka'}
gatchina {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
gelendzhik {'scooters', 'lavka'}
gelendzhik_airport set()
georgievsk {'scooters', 'eda', 'lavka'}
glazov {'scooters', 'eda', 'lavka'}
golicyno {'vezeteconom', 'cargocorp', 'express', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'comfortplus', 'courier'}
gomel {'lavka'}
gomel_region {'eda'}
goris {'eda'}
gorno-altaysk {'scooters', 'eda', 'lavka'}
gornyj {'vezeteconom', 'eda'}
goryachiy_kluch {'scooters', 'eda', 'lavka'}
grodno {'lavka'}
grodno_region {'eda'}
grozniy {'scooters', 'eda', 'lavka'}
gubakha {'scooters', 'eda', 'lavka'}
gukovo {'scooters', 'eda', 'lavka'}
gus-chrustalniy {'scooters', 'eda', 'lavka'}
gusev {'scooters', 'eda', 'lavka'}
gvardeysk {'eda'}
gyumri {'eda'}
gyumri_to_yerevan {'eda', 'econom'}
hanty_mansijsk {'scooters', 'eda', 'lavka'}
helsinki {'eda'}
himki {'scooters', 'universal', 'drive', 'promo'}
hotkovo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
ida-virumaa {'eda'}
iglino {'scooters', 'eda', 'lavka'}
ilinskiy {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
ilskiy {'scooters', 'eda', 'lavka'}
irbit {'scooters', 'eda', 'lavka'}
irkutsk {'scooters', 'night', 'cargocorp', 'drive'}
ishim {'scooters', 'eda', 'lavka'}
ishimbay {'scooters', 'eda', 'lavka'}
iskitim {'scooters', 'eda', 'lavka'}
israel_ashdod {'eda', 'econom'}
israel_ashkelon {'eda', 'econom'}
israel_beersheba {'eda', 'econom'}
israel_haifa {'eda', 'econom'}
istra {'scooters', 'cargocorp', 'drive', 'promo'}
ivacevichi {'eda'}
ivanovo {'cargocorp', 'lavka', 'promo', 'scooters', 'night', 'drive', 'premium_suv'}
ivanovo_region {'eda'}
ivanteevka {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
ivanteyevka_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
izberbash {'scooters', 'eda', 'lavka'}
izhevsk {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
johannesburg {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
jurmala {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
kalach {'scooters', 'eda', 'lavka'}
kalach_na_donu {'scooters', 'eda', 'lavka'}
kalininec {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'courier'}
kaliningrad {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
kaliningrad_region {'eda'}
kaltan {'vezeteconom', 'eda'}
kaluga {'cargocorp', 'lavka', 'scooters', 'night', 'drive', 'mkk_antifraud'}
kaluga_region {'eda'}
kamen-na-obi {'scooters', 'eda', 'lavka'}
kamensk-shakhtinsky {'scooters', 'eda', 'lavka'}
kamenskuralsky {'scooters', 'eda', 'lavka'}
kamyshin {'scooters', 'eda', 'lavka'}
kamyzyak {'eda'}
kanash {'scooters', 'eda', 'lavka'}
kanevskaja {'scooters', 'eda', 'lavka'}
kapan {'eda'}
karachaevo_cherkesiya_region {'eda'}
karaganda {'eda'}
karelia_region {'eda'}
karmaskaly {'vezeteconom', 'eda'}
kashira {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
kaspiysk {'scooters', 'eda', 'lavka'}
kaunas {'eda'}
kazan {'start', 'promo', 'scooters', 'mkk_antifraud', 'uberlux'}
kemerovo {'scooters', 'cargocorp', 'drive'}
kemerovo_region {'eda'}
khabarovsk {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
khabarovsk_region {'eda'}
khakassia_region {'eda'}
kharkiv {'eda'}
khasavurt {'scooters', 'eda', 'lavka'}
kinel {'scooters', 'eda', 'lavka'}
kineshma {'scooters', 'eda', 'lavka'}
kirov {'scooters', 'lavka'}
kirovochepetsk {'scooters', 'eda', 'lavka'}
kirzach {'scooters', 'eda', 'lavka'}
kishinev {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
kislovodsk {'scooters', 'lavka'}
kizil {'scooters', 'eda', 'lavka'}
kizilyurt {'scooters', 'eda', 'lavka'}
klimovsk {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
klin {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
kobrin {'eda'}
kogalym {'scooters', 'eda', 'lavka'}
kokshetau {'eda'}
kolchugino {'scooters', 'eda', 'lavka'}
kolomna {'scooters', 'cargocorp', 'drive', 'promo'}
kolpino {'scooters', 'cargocorp', 'drive'}
kolyvan {'vezeteconom', 'eda'}
komi_region {'eda'}
komsomolsknaamure {'scooters', 'eda', 'lavka'}
kondrovo {'eda'}
konstantinovsk {'scooters', 'eda', 'lavka'}
korenovsk {'scooters', 'eda', 'lavka'}
korkino {'eda'}
korolev {'scooters', 'drive', 'promo'}
korolev_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
kostanai {'eda'}
kostroma {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
kostroma_region {'eda'}
kotayk_region {'eda'}
kotelniki {'scooters', 'drive', 'promo'}
kovrov {'scooters', 'eda', 'lavka'}
kozelsk {'eda'}
kozmodemyansk {'scooters', 'eda', 'lavka'}
kraskovo {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
krasnayapolyana set()
krasnoarmeysk {'scooters', 'cargocorp', 'drive', 'promo'}
krasnoarmeysk_saratov {'eda'}
krasnoarmeysky_volgograd {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
krasnodar {'start', 'promo', 'drive', 'mkk_antifraud', 'uberlux'}
krasnodar_region {'eda'}
krasnoe_selo {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
krasnogorsk {'scooters', 'drive', 'promo'}
krasnogorsk_district {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'universal'}
krasnogorsky_district {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
krasnoyarsk {'lavka', 'promo', 'scooters', 'night', 'drive', 'mkk_antifraud', 'uberlux'}
krasnoyarsk_region {'eda'}
krasnoznamensk {'scooters', 'cargocorp', 'drive', 'promo'}
kratovo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
krilovskaya {'scooters', 'eda', 'lavka'}
krivoirog {'eda'}
kronstadt set()
kropotkin {'scooters', 'eda', 'lavka'}
krymsk {'scooters', 'eda', 'lavka'}
kstovo {'cargocorp', 'lavka', 'scooters', 'eda', 'drive', 'premium_suv'}
kubinka {'scooters', 'cargocorp', 'drive', 'promo'}
kudimkar {'scooters', 'eda', 'lavka'}
kumasi {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
kumertau {'scooters', 'eda', 'lavka'}
kungur {'scooters', 'eda', 'lavka'}
kungur_district {'eda'}
kurchatov {'scooters', 'eda', 'lavka'}
kurgan {'scooters', 'eda', 'lavka'}
kurgan_region {'vezeteconom', 'eda'}
kurganinsk {'scooters', 'eda', 'lavka'}
kurortny_district {'eda'}
kurovskoye {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
kursk {'scooters', 'cargocorp', 'lavka', 'drive'}
kursk_region {'eda'}
kushevskaya {'scooters', 'eda', 'lavka'}
kutaisi {'eda'}
kutaisi_airport {'eda'}
kyiv {'eda'}
kyzylorda {'eda'}
labinsk {'scooters', 'eda', 'lavka'}
lazarevskoye {'cargocorp', 'start', 'lavka', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
leninigorsk {'scooters', 'eda', 'lavka'}
lensk {'cargocorp', 'lavka', 'scooters', 'shuttle', 'eda', 'drive', 'walking_courier_for_performer'}
lepel {'eda'}
lesnoj_gorodok {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
lida {'eda'}
likino_dulyovo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
lipetsk {'cargocorp', 'lavka', 'scooters', 'night', 'drive'}
lipetsk_region {'eda'}
lisky {'scooters', 'eda', 'lavka'}
lobnja {'scooters', 'cargocorp', 'drive', 'promo'}
lobnya_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
lomonosov {'scooters', 'cargocorp', 'eda', 'drive', 'lavka'}
london {'scooters', 'eda', 'courier', 'econom'}
losino-petrovsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
losino_petrovsky {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
lukhovitsy {'scooters', 'cargocorp', 'drive', 'promo'}
lukoyanov {'scooters', 'eda', 'lavka'}
lviv {'eda'}
lvovskij {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'courier'}
lyberci {'scooters', 'drive', 'promo'}
lysva {'scooters', 'eda', 'lavka'}
lytkarino {'scooters', 'cargocorp', 'drive', 'promo'}
lytkarino_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
lyudinovo {'eda'}
magadan {'scooters', 'eda', 'lavka'}
magas {'scooters', 'eda', 'lavka'}
magnitogorsk {'scooters', 'lavka', 'drive', 'promo'}
maikop {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
makhachkala {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
malahovka {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
malino {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
malorita {'eda'}
mariel_region {'eda'}
marks {'eda'}
matveev_kurgan {'scooters', 'eda', 'lavka'}
meleuz {'scooters', 'eda', 'lavka'}
mendeleevo {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'courier'}
mezgdurechensk {'eda'}
miass {'scooters', 'lavka'}
michurinsk {'scooters', 'eda', 'lavka'}
mihaylovka {'scooters', 'eda', 'lavka'}
mikhaylovsk set()
mikhnevo {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
minsk {'lavka'}
minsk_region {'eda'}
minusinsk {'scooters', 'eda', 'lavka'}
mirny {'cargocorp', 'lavka', 'scooters', 'shuttle', 'eda', 'drive', 'walking_courier_for_performer'}
mogilev set()
molodcheno {'eda'}
monino {'scooters', 'cargocorp', 'drive', 'promo'}
mordoviya_region {'eda'}
moscow {'mkk_antifraud', 'universal', 'promo'}
mosti {'eda'}
mozhaysk {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
mozhga {'scooters', 'eda', 'lavka'}
mozyr {'eda'}
mtsensk {'scooters', 'eda', 'lavka'}
murmansk {'scooters', 'lavka'}
murmansk_region {'eda'}
murom {'scooters', 'eda', 'lavka'}
myneralnyevody {'scooters', 'eda', 'lavka'}
myneralnyevody_airport {'eda'}
myski {'eda'}
mytishchi {'scooters', 'drive', 'promo'}
mytishchi_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
naberezhnyechelny {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
nakhabino {'scooters', 'cargocorp', 'drive', 'promo'}
nakhodka {'scooters', 'eda', 'lavka'}
nalchik {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
namangan {'eda', 'econom'}
narofominsk {'scooters', 'cargocorp', 'drive', 'promo'}
nartkala {'scooters', 'eda', 'lavka'}
narva {'eda'}
neftekamsk {'cargocorp', 'lavka', 'scooters', 'night', 'eda', 'drive'}
neftekumsk {'scooters', 'eda', 'lavka'}
nefteyugansk {'scooters', 'eda', 'lavka'}
nekrasovskij {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv'}
nesvizh {'eda'}
nevinnomissk {'scooters', 'eda', 'lavka'}
nizhnekamsk {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
nizhnevartovsk {'scooters', 'lavka'}
nizhnynovgorod {'scooters', 'mkk_antifraud', 'drive', 'promo'}
nizhnynovgorod_region {'eda'}
nizhnytagil {'scooters', 'lavka'}
noginsk {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
norilsk {'scooters', 'eda', 'lavka'}
novgorod_region {'eda'}
novi_sad {'eda'}
novoaltaysk {'scooters', 'eda', 'lavka'}
novocherkassk {'scooters', 'eda', 'lavka'}
novogrudok {'eda'}
novokuibishevsk {'scooters', 'eda', 'lavka'}
novokuznetsk {'scooters', 'lavka'}
novomoskovsk {'scooters', 'eda', 'lavka'}
novorossiysk {'scooters', 'lavka'}
novosibirsk {'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
novosibirsk_region {'eda'}
novotroick {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
novoulianovsk {'eda'}
novouralsk {'scooters', 'eda', 'lavka'}
novozibkov {'scooters', 'eda', 'lavka'}
novyurengoy {'scooters', 'eda', 'lavka'}
noyabrsk {'scooters', 'eda', 'lavka'}
nyagan {'scooters', 'eda', 'lavka'}
obninsk {'scooters'}
obuhovo {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
odessa {'eda'}
odincovo {'scooters', 'drive', 'promo'}
odincovo_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
odintsovskii_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
oktyabrsky {'scooters', 'eda', 'lavka'}
oktyabrsky_mo {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
omsk {'lavka', 'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
omsk_region {'eda'}
orehovozuevo {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
orel {'scooters', 'cargocorp', 'lavka', 'drive'}
orel_region {'eda'}
orenburg {'cargocorp', 'lavka', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
orenburg_region {'eda'}
orsha {'eda'}
orsk {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
osa {'scooters', 'eda', 'lavka', 'courier'}
osetia_region {'eda'}
osh {'eda'}
osinniki {'eda'}
oslo {'scooters', 'comfort', 'eda'}
ostrogozhsk {'scooters', 'eda', 'lavka'}
otradnyy {'scooters', 'eda', 'lavka'}
ozersk {'scooters', 'eda', 'lavka'}
ozery {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
paris {'scooters', 'eda', 'courier', 'econom'}
pavlodar {'eda'}
pavlovsk {'cargocorp', 'lavka', 'scooters', 'night', 'eda', 'drive'}
pavlovskyposad {'scooters', 'cargocorp', 'drive', 'promo'}
penza {'scooters', 'drive', 'lavka', 'promo'}
penza_region {'eda'}
perm {'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
petergof {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
petropavlovsk {'eda'}
petropavlovskkamchatskiy {'scooters', 'eda', 'lavka'}
petrozavodsk {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
pinsk {'eda'}
pionersky {'eda'}
pjatygorsk {'scooters', 'lavka'}
platov_airport {'lavka'}
podolsk {'scooters', 'drive', 'promo'}
podolsk_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
polevskoy {'scooters', 'eda', 'lavka'}
polotsk {'eda'}
pravdinskij {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
primorskij_region {'eda'}
primorsko-ahtars {'scooters', 'eda', 'lavka', 'courier'}
privolzhskiy {'eda'}
prohladny {'scooters', 'eda', 'lavka'}
prokopyevsk {'scooters', 'eda', 'lavka'}
protvino {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
pruzhany {'eda'}
pskov {'scooters', 'lavka'}
pskov_region {'eda'}
pushino {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'suv'}
pushkin {'scooters', 'night', 'cargocorp', 'drive'}
pushkino {'scooters', 'drive', 'promo'}
pushkinsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
ramenskoe {'cargocorp', 'promo', 'scooters', 'night', 'drive'}
ramensky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
rasskazovo {'scooters', 'eda', 'lavka'}
rechitsa {'eda'}
reutov {'scooters', 'drive', 'promo'}
revda {'scooters', 'eda', 'lavka'}
riga {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
rodniki_mo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'courier'}
roshal {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
roslavl {'scooters', 'eda', 'lavka'}
rossosh {'scooters', 'eda', 'lavka'}
rostov {'scooters', 'eda', 'lavka'}
rostovondon {'start', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
rostovondon_region {'eda'}
rubtsovsk {'scooters', 'eda', 'lavka'}
rustavi {'eda'}
ruza {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
ruzaevka {'scooters', 'eda', 'lavka'}
ryazan {'scooters', 'mkk_antifraud', 'drive', 'promo'}
ryazan_region {'eda'}
rybinsk {'scooters', 'eda', 'lavka'}
rzhev {'scooters', 'eda', 'lavka'}
safonovo {'scooters', 'eda', 'lavka'}
salavat {'scooters', 'eda', 'lavka'}
salekhard {'scooters', 'eda', 'lavka'}
salsk {'scooters', 'eda', 'lavka'}
samara {'start', 'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
samara_airport {'scooters', 'eda', 'lavka'}
samara_region {'eda'}
santiago {'eda', 'econom'}
saransk {'cargocorp', 'lavka', 'scooters', 'night', 'drive'}
sarapul {'scooters', 'eda', 'lavka'}
saratov {'cargocorp', 'lavka', 'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
saratov_region {'eda'}
sarov {'scooters', 'eda', 'lavka'}
sayanogorsk {'scooters', 'eda', 'lavka'}
schelkovsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
selyatino {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
semey {'eda'}
semikarakorsk {'scooters', 'eda', 'lavka'}
sengiley {'vezeteconom', 'eda'}
sergievposad {'scooters', 'cargocorp', 'drive', 'promo'}
serpukhov {'scooters', 'cargocorp', 'drive', 'promo'}
sertolovo {'scooters', 'cargocorp', 'drive'}
sestroretsk {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
severodvinsk {'scooters', 'eda', 'lavka'}
severomorsk {'scooters', 'eda', 'lavka'}
seversk {'scooters', 'eda', 'lavka'}
severskaya {'scooters', 'eda', 'lavka'}
shadrinsk {'scooters', 'eda', 'lavka'}
shakhty {'scooters', 'lavka'}
shatura {'scooters', 'cargocorp', 'drive', 'promo'}
shcherbinka {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
shelkovo {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
shodnya {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
shuya {'scooters', 'eda', 'lavka'}
sibaj {'scooters', 'eda', 'lavka'}
slavyansk-na-kubani {'scooters', 'eda', 'lavka'}
slobodskoy {'eda'}
slonim {'eda'}
slutsk {'eda'}
smolensk {'scooters', 'lavka'}
smolensk_region {'eda'}
sochi {'start', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
sochi_airport set()
sofrino {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
solihorsk {'eda'}
solikamsk {'scooters', 'eda', 'lavka'}
solnechnogorsk {'scooters', 'cargocorp', 'drive', 'promo'}
sorochinsk {'scooters', 'eda', 'lavka'}
sovetsk {'eda'}
sovetsky {'scooters', 'eda', 'lavka'}
spb {'promo', 'scooters', 'night', 'mkk_antifraud', 'uberlux'}
spb_airport {'scooters', 'cargocorp', 'courier', 'mkk_antifraud'}
spb_region {'eda'}
staraja_kupavna {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
staraya_russa {'scooters', 'eda', 'lavka'}
stariyoskol {'scooters', 'lavka'}
stavropol {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
stavropol_airport {'scooters', 'lavka', 'courier'}
stavropol_region {'eda'}
stepnoe {'vezeteconom', 'eda'}
sterlitamak {'scooters', 'lavka'}
stolbtsy {'eda'}
stroitel {'scooters', 'eda', 'lavka'}
stupino {'scooters', 'cargocorp', 'drive', 'promo'}
surgut {'scooters', 'cargocorp', 'lavka', 'drive'}
sverdlovsk_region {'eda'}
sverdlovsky {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
svetlogorsk {'eda'}
svetlogorsk_gomel {'eda'}
svetlograd {'scooters', 'eda', 'lavka'}
svo {'scooters', 'cargocorp', 'courier', 'promo'}
svobodnyy {'scooters', 'eda', 'lavka'}
syktyvkar {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
sysert {'scooters', 'eda', 'lavka'}
syzran {'scooters', 'eda', 'lavka'}
taganrog {'scooters', 'lavka'}
taldom {'eda'}
taldykorgan {'eda'}
tallinn {'eda'}
tamale {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
tambov {'scooters', 'lavka'}
tampere {'eda'}
taraz {'eda'}
tarko_sale {'scooters', 'eda', 'lavka'}
tartu {'eda'}
tashkent {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
tatarstan {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
tbilisi {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
tel_aviv {'econom', 'scooters', 'ultimate', 'drive', 'universal'}
temirtau {'eda'}
temryuk {'scooters', 'eda', 'lavka', 'courier'}
timashevsk {'scooters', 'eda', 'lavka'}
tixoretsk {'scooters', 'eda', 'lavka'}
tobolsk {'scooters', 'eda', 'lavka'}
togliatti {'cargocorp', 'lavka', 'promo', 'scooters', 'drive', 'mkk_antifraud'}
toksovo set()
tomilino {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
tomsk {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
tomsk_region {'eda'}
troick {'scooters', 'cargocorp', 'drive', 'promo'}
troitsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
tuapse {'scooters', 'eda', 'lavka'}
tuchkovo {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
tula {'cargocorp', 'lavka', 'promo', 'scooters', 'night', 'drive'}
tumen {'cargocorp', 'promo', 'scooters', 'night', 'drive', 'mkk_antifraud'}
tumen_region {'eda'}
turku {'eda'}
tutaev {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
tuymazy {'scooters', 'eda', 'lavka'}
tver {'scooters', 'lavka'}
tver_region {'eda'}
udelnaya {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
ufa {'start', 'promo', 'scooters', 'night', 'drive', 'standart', 'mkk', 'mkk_antifraud'}
ugorsk {'scooters', 'eda', 'lavka'}
uhta {'scooters', 'eda', 'lavka'}
ulanude {'cargocorp', 'lavka', 'scooters', 'night', 'eda', 'drive'}
ulianovsk {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
ulianovsk_airport set()
ulianovsk_region {'eda'}
uralsk {'eda'}
uryupinsk {'scooters', 'eda', 'lavka'}
usinsk {'scooters', 'eda', 'lavka'}
ussuriysk {'scooters', 'eda', 'lavka'}
ust_kamenogorsk {'eda'}
ust_kurdyum {'eda'}
ustlabinsk {'scooters', 'eda', 'lavka'}
vanadzor {'eda'}
vayots_dzor {'eda'}
velikie_luky {'scooters', 'eda', 'lavka'}
velikynovgorod {'scooters', 'lavka'}
verhnya_salda {'scooters', 'eda', 'lavka'}
verzilovo {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
vidnoe {'scooters', 'drive', 'promo'}
vidnoe_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
vileyka {'eda'}
vilnius {'eda'}
viselki {'scooters', 'eda', 'lavka'}
vishniy_volochek {'scooters', 'eda', 'lavka'}
vitebsk set()
vko {'scooters', 'cargocorp', 'promo'}
vladikavkaz {'scooters', 'lavka'}
vladimir {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
vladimir_region {'eda'}
vladivostok {'scooters', 'cargocorp', 'drive'}
vlasiha {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
vniissok {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv', 'courier'}
volgodonsk {'scooters', 'eda', 'lavka'}
volgograd {'scooters', 'mkk_antifraud', 'drive', 'promo'}
volgograd_airport {'lavka'}
volgograd_region {'eda'}
volkovysk {'eda'}
vologda {'scooters', 'drive', 'cargocorp', 'lavka'}
vologda_region {'eda'}
volokolamsk {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
volsk {'scooters', 'eda', 'lavka'}
volzhsk {'scooters', 'eda', 'lavka'}
volzhskiy {'scooters', 'cargocorp', 'lavka', 'drive'}
voronezh {'scooters', 'mkk_antifraud', 'drive', 'promo'}
voronezh_region {'eda'}
voskresensk {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
voskresenskydistrict {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
votkinsk {'scooters', 'eda', 'lavka'}
vsevolozhsk {'scooters', 'cargocorp', 'drive'}
vyazma {'scooters', 'eda', 'lavka'}
vyazniki {'scooters', 'eda', 'lavka'}
vyksa {'scooters', 'eda', 'lavka'}
yahroma {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
yakutsk {'cargocorp', 'lavka', 'scooters', 'eda', 'drive'}
yaounde {'eda'}
yaroslavl {'scooters', 'night', 'drive', 'promo'}
yartsevo {'scooters', 'eda', 'lavka'}
yelets {'scooters', 'eda', 'lavka'}
yerevan {'cargocorp', 'econom', 'lavka', 'scooters', 'eda', 'drive'}
yerevan_airport {'eda', 'econom'}
yesk {'scooters', 'eda', 'lavka'}
yoshkarola {'cargocorp', 'lavka', 'promo', 'scooters', 'drive'}
yurga {'scooters', 'eda', 'lavka'}
yuzhnosakhalinsk {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive'}
zapolyarni {'scooters', 'eda', 'lavka'}
zaraysk {'vezeteconom', 'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
zaraysk_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
zarechny {'scooters', 'eda', 'lavka'}
zarechny_penza {'eda'}
zavety_il'icha {'cargocorp', 'lavka', 'promo', 'scooters', 'eda', 'drive', 'premium_suv', 'suv'}
zavoljie {'scooters', 'eda', 'lavka'}
zelenodolsk {'scooters', 'eda', 'lavka'}
zelenograd {'scooters', 'cargocorp', 'drive', 'promo'}
zelenogradsk {'scooters', 'eda', 'lavka'}
zelenogradsk_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
zheleznodorozhny {'scooters', 'cargocorp', 'drive', 'promo'}
zheleznogorsk {'scooters', 'eda', 'lavka'}
zhezkazgan {'eda'}
zhiguliovsk {'scooters', 'eda', 'lavka'}
zhlobin {'eda'}
zhodino {'eda'}
zhukovskiy {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
zhukovsky_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
zlatoust {'scooters', 'eda', 'lavka'}
zvenigorod {'cargocorp', 'promo', 'scooters', 'drive', 'premium_suv'}
zvenigorod_district {'scooters', 'cargocorp', 'eda', 'drive', 'premium_suv', 'lavka', 'promo'}
```

</details>


## Где используется 

* [uservices](https://a.yandex-team.ru/arc_vcs/taxi/uservices/libraries/tariff-categories-visibility/src/checks.cpp?rev=r8537228#L141)
* [backend-cpp](https://github.yandex-team.ru/taxi/backend-cpp/blob/076a31c06bfd862865f5d279cea30a15e6bab899/common/src/config/classes_config.cpp#L329)
* [backend-py3](https://a.yandex-team.ru/arc_vcs/taxi/backend-py3/services/taxi-corp/taxi_corp/stuff/update_experiments.py?rev=r8925200#L221)

# Как решаем проблему

Конфиг в соответсвии со схемой 
сопоставляет зоне и тарифу (категории) 
следующие аттрибуты:

| Аттрибут               |   Тип   |
|------------------------|:-------:|
| visible_by_default     | boolean |
| visible_on_site        | boolean |
| use_legacy_experiments | boolean |
| show_experiment        | string  |
 | hide_experiment        | string  |

Данные поля планируется перенести в существующую коллеккцию `tariff_settings` в объект `s` 
и связать с соответвующими категориями. Значение use_legacy_experiments в текущей конфигурации 
не используется, его не переносим.
<details>
  <summary>Пример такой категории в аттрибуте `s` в базе `tariff_settings`</summary>

```
 {
   "card_payment_settings": {
     "max_refund": new NumberInt("9000"),
     "max_compensation": new NumberInt("9000")
   },
   "toll_roads_enabled": true,
   "cc": [
   ],
   "d_zone_leave": false,
   "oso": true,
   "d_dest_change": false,
   "branding_id": "econom_region",
   "mark_as_new": false,
   "e_leg_ent": true,
   "max_card_payment": new NumberInt("3200"),
   "persistent_reqs": [
   ],
   "rd": false,
   "glued_requirements": [
   ],
   "tc": [
   ],
   "max_corp_payment": new NumberInt("5000"),
   "fct": new NumberInt("300"),
   "fixed_price_enabled": false,
   "nos": [
     {
       "c": new NumberInt("3"),
       "tr": {
         "text": "tariffs.notification.antisurge_clarification.text",
         "button": "tariffs.notification.antisurge_clarification.button",
         "title": "tariffs.notification.antisurge_clarification.title"
       },
       "k": "antisurge_clarification",
       "t": "tariff_popup"
     },
     {
       "c": new NumberInt("3"),
       "tr": {
         "text": "tariffs.notification.altpin_clarification.text",
         "button": "tariffs.notification.altpin_clarification.button",
         "title": "tariffs.notification.altpin_clarification.title"
       },
       "k": "altpin_clarification",
       "t": "tariff_popup"
     }
   ],
   "d_ban_feedback": false,
   "d": true,
   "comments_disabled": false,
   "n": "econom",
   "r": true,
   "d_live_loc": false,
   "t": "name.econom",
   "sl": [
     new NumberInt("50")
   ],
   "client_requirements": [
     "animaltransport",
     "childchair_kazan"
   ]
 },
 ```

</details>


## Изменения в админке
В админке на странице тарифов для зоны предполагается добавить новый блок (см. макет).

![image](static/visibility.png)

Для отображения нового блока будет расширен api существующих ручек:
* [get:   /api/tariff_settings/{zone_name}/](https://github.yandex-team.ru/taxi/backend/pull/14200/files#diff-37af000fa05e37c49d7fcd436ef1dc804a94a375917e902df9e5b8cf002d1fd9L19)
* [post:  /api/set_tariff_settings/{zone_name}/](https://github.yandex-team.ru/taxi/backend/pull/14200/files#diff-37af000fa05e37c49d7fcd436ef1dc804a94a375917e902df9e5b8cf002d1fd9L19)

Изменения затрагивают объект `Category` из схемы 
[tariff_settings.yaml](https://github.yandex-team.ru/taxi/backend/pull/14200/files#diff-37af000fa05e37c49d7fcd436ef1dc804a94a375917e902df9e5b8cf002d1fd9):
 ```
visible_by_default:
   description: Видимость категории по умолчанию
   type: boolean
show_experiment:
   descriprion: Эксперимент разрешающий видимость
   type: string
hide_experiment:
   descriprion: Эксперимент запрещающий видимость
   type: string
visible_on_site:
   description: Видимость каатегории на сайте такси
   type: boolean
 ```
<details>
  <summary>Пример нового запроса через approvals</summary>

```
data='{
    "request_id": "93bb060748ef4c5daf9bea1a8cde879e",
    "change_doc_id": "93bb060748ef4c5daf9bea1a8cde879e",
    "run_manually": false,
    "data": {
.............
        "categories": [
            {
.............
                "category_name": "econom",
                "legal_entities_enabled": true,
                "visible_by_default": true,
                "show_experiment": "example_show_experiment",
                "hide_experiment": "example_hide_experiment",
                "visible_on_site": true
            },
.............
        ],
        "layout": "default",
        "max_route_points_count": 50.0,
        "country": "rus",
        "paid_cancel_enabled": true,
        "is_beta": false,
        "client_exact_order_round_minutes": 1
    },
.............
}'
```

</details>


## Изменения в uservices
Основная идея доработать  ручку `/v1/tariff_settings/bulk_retrieve` 
и добавить для каждой категории аттрибуты из таблицы выше. 
Тут стоит подключить либу taxi-tariffs, там уже есть кэш тарифов. 
Под экспериментом перевести логику с использования конфига `TARIFF_CATEGORIES_VISIBILITY` 
на значения из кеша `taxi-tariffs` там где это требуется

* [Ссылка 1](https://a.yandex-team.ru/arc_vcs/taxi/uservices/libraries/tariff-categories-visibility/src/checks.cpp?rev=r8537228#L135)
* [Ссылка 2](https://a.yandex-team.ru/arc_vcs/taxi/uservices/libraries/taxi-tariffs/src/caches/tariff_settings.cpp?rev=r9085472#L81)

## Изменения в backend-cpp
Здесь аналогичный подход, переключиться 
на использование кэша тарифов под экспериментом, 
доработать следующие места:

* [Ссылка 1](https://github.yandex-team.ru/taxi/backend-cpp/blob/58c463678473b7608aa48140884d920db1a242a5/common/src/models/tariffs.cpp#L250)
* [Ссылка 2](https://github.yandex-team.ru/taxi/backend-cpp/blob/58c463678473b7608aa48140884d920db1a242a5/common/src/models/tariffs.cpp#L301)
* [Ссылка 3](https://github.yandex-team.ru/taxi/backend-cpp/blob/47df5f4cdddc73cddf63ddece1671e011e303fd7/protocol/lib/src/views/routestats/response.cpp#L1638)
* [Ссылка 4](https://github.yandex-team.ru/taxi/backend-cpp/blob/076a31c06bfd862865f5d279cea30a15e6bab899/protocol/lib/src/views/tariffs/tariffs.cpp#L359)

## Изменения в backend-py3
 Здесь выполняется создание драфта на изменения конфига, переключится на новое создание драфта видимости