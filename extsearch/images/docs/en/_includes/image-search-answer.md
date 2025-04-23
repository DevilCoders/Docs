# Image search response

The image search API returns an XML response. Results are provided in the form of XML elements.

The XML documents consist of the grouping tags [request]{% if audience == "internal" %}(../concepts/requestelement-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#requestelement){% endif %} (summarized information about the query) and [response]{% if audience == "internal" %}(../concepts/responseel-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#responseel){% endif %} (a list of search results for the query).

Below, you can see the general structure of the XML output.

```xml
<yandexsearch version="1.0">
   <request>
      <!--Request attributes are in child tags-->
   </request>
   <response>
      <!--General information about getting search results is in the child tags-->
      <reask>
         <!--Information about text automatically replaced in the query before searching. Only added if the query was corrected-->
      </reask>
      <results>
         <!--Grouping parameters and search results are in child tags-->
         <grouping attr="ii" mode="deep" groups-on-page="20" docs-in-group="1" curcateg="-1">
         <group>
         <!--Information about a single image search result. Contains information about the image returned for output, and its duplicates. Non-grouping child tags contain general information about a group-->
            <doc>
               <!--Information about a found image and its duplicates is in child tags-->
            </doc>  
               <image-properties>
                  <!--Properties of images displayed in search results are in child tags-->
               </image-properties>
               <image-duplicates>
                  <!--Information about duplicates of the image displayed in search results. Information about each duplicate is contained in child tags of the grouping tag image-properties-->
               </image-duplicates>
               <image-duplicates-fitsize>
                  <!--Information about full-size duplicates found. Information about each duplicate is contained in child tags of the grouping tag image-properties-->
               </image-duplicates-fitsize>
               <image-duplicates-preview>
                  <!--Information about preview-sized copies of the image found. Information about each duplicate is found in child tags of the grouping tag image-properties-->
               </image-duplicates-preview>
         </group>
         <group>
         </group>
         ...
         <group>
         </group>
   </response>
```