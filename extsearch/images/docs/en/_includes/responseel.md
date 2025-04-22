## The response element {#responseel}

The `response` element contains search results for the query that information is provided for in the [request]{% if audience == "internal" %}(../concepts/requestelement-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#requestelement){% endif %} element.

Contains the `date` attribute, which is the request date and time in the format `<year><month><day>Т<hour><minute><second>` for UTC.

The element contains the following sections:

- [Overview of search results](#basicinfo).
- [The “reask” block](#reaskblock).
- [The “results” block](#resultsblock).

### Overview of search results {#basicinfo}

Tags for the search results overview block are shown in the table below.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `error` | Error description.

XML is added only if an error occurs. | `code` — Error ID. ||
|| `reqid` |  Unique request ID. | No attributes. || 
|| `wordstat` | The frequency at which the query words occur in the search index, in the format:

```
<word 1>: <word 1 frequency>,<word 2>: <word 2 frequency>,...,<word n>: <word n frequency> 
```

The `n` value corresponds to the number of words in the query. | No attributes. ||
|| `found` | The number of images found for each degree of relevancy. Relevancy is determined by the value of the `priority` attribute. | `priority` — Degree to which results match the query.

Possible values:

- “phrase” — Number of documents with an exact occurrence of the search query.
- “strict” — Number of documents that contain the query words.
- “all” — Total number of documents found.

Values passed in the tag must be the same for all values of the attribute. ||
|| `found-human` | A string in Russian containing information about the number of images found and accompanying text. | No attributes. || 
{% if audience == "internal" %}|| `is-local` | Service attribute.

Shown only when the request is made from the internal Yandex network. | No attributes. ||{% endif %}
|#

### The “reask” block {#reaskblock}

Optional. Present only if a spelling mistake was corrected in the query.

The `reask` block tags are shown in the table below.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `rule` | Type of correction made to the query. Possible values:

`Misspell` — Spelling mistake.

`KeyboardLayout` — Wrong keyboard layout was used. | No attributes. ||
|| `source-text` | Original query text. | No attributes. ||
|| `hlword` | Highlighted part of the query. | No attributes. ||
|| `text-to-show` | The corrected query text in the correct language. Usually matches the value of the `text` tag. | No attributes. ||
|| `text` | The corrected query text. | No attributes. ||
|#


### The “results” block {#resultsblock}

Optional. Present only if results were found for the query.

Contains details on images found. The beginning of the block contains general information about search results and grouping parameters. Information about each found image is contained in the `group` tags.

The table below shows information about the `results` block tags.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `grouping` | Rules for grouping found images. | 
- `attr`— Types of sources used. Must have the value “ii”.
- `mode` — Type of grouping.
- `groups-on-page` — Number of search results that can be displayed on a single page.
- `docs-in-group` — Number of images in a group. Must have the value “1”.
- `curcateg` — Service attribute. Must have the value “-1”. ||
|| `found` | The number of image groups found for each degree of relevancy.

Currently, each group of images contains a single image.

The degree of relevancy is determined by the value of the `priority` attribute. | `priority` — Degree to which results match the query. Possible values:

- “phrase” — Number of documents with an exact occurrence of the search query.
- “strict” — Number of documents that contain the query words.
- “all” — Total number of documents found. ||
|| `found-docs` | The number of documents containing the found images for each degree of relevancy.

Since each group of images contains a single image, the values of the `found` and `found-docs` tags should match.

Relevancy is determined by the value of the `priority` attribute. | `priority` — Degree to which results match the query. Possible values:

- “phrase” — Number of documents with an exact occurrence of the search query.
- “strict” — Number of documents that contain the query words.
- “all” — Total number of documents found. ||
|| `found-docs-human` | A string in Russian containing information about the number of images found and accompanying text. | No attributes. ||
|#

> The `group` grouping tag. Each tag contains information about the image group found and the image duplicates. Since each group of images contains a single image, the tag provides information about one image and its duplicates. No attributes.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `categ` | 	Description of the found image. | 
- `attr` — Name of the grouping. Matches the value of the `attr` attribute for the [groupby]{% if audience == "internal" %}(../concepts/requestelement-internal.md#requestgroupby){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#requestgroupby){% endif %} tag of the [request]{% if audience == "internal" %}(../concepts/requestelement-internal.md){% endif %}{% if audience == "external" %}(../concepts/xmlanswer.md#requestelement){% endif %} element.
- `name` — Name of the main host where the image is stored. ||
|| `doccount` | 	Service tag. 

{% if audience == "internal" %}

Lower estimate of the number of images found in the image group. Since each image group contains a single image, this tag always has the value “1”.

{% endif %} | No attributes. ||
|| `relevance` | Service tag. 

{% if audience == "internal" %}

The relevancy value for a group of images.

{% endif %} | `priority` — Service attribute. ||
|#

> The `doc` grouping tag. Each tag contains information about a found image and its duplicates. Contains the `id` attribute, the image ID.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `relevance` | Service tag. 

{% if audience == "internal" %}

The relevancy value for an image.

{% endif %} | `priority` — Service attribute. ||
|| `url` | The address where the image is available. | No attributes. ||
|| `domain` | The domain where the document that contains the image is located. | No attributes. ||
|| `title` | Service tag. 

{% if audience == "internal" %}

Image title. Not used in output. May contain selected fragments in `hlword` tags.

{% endif %} | No attributes. ||
|| `modtime` | The data and time when the image was modified, in the format:

`<year><month><day>Т<hour><minute><second>` | No attributes. ||
|| `size` | Image size, in bytes. |	No attributes. || 
|| `charset` | The encoding of the document that contains the image. |	No attributes. ||
|| `passages` | Container for a list of snippets for the image. 

Images always have one snippet generated. |	No attributes. ||
|| `passage` | Snippet for the image. Query words are selected by the `hlword` tag. |	No attributes. ||
|| `properties` | A container for document properties. |	No attributes. ||
|| `ClipsProperties` | Service tag. Contains the field values of the XML document in serialized form. |	No attributes. ||
{% if audience == "internal" %}|| `DESC` | Service tag.

Contains a brief description of the object found. | No attributes. ||{% endif %}
|| `FeaturedClips` | Service tag. Contains the field values of the XML document in serialized form. |	No attributes. ||
{% if audience == "internal" %}||`HasImageSignature` | Whether the image has a signature for searching for similar images. 

Possible values: 
- “0” — No signature.
- “1” — Has a signature. | No attributes. ||{% endif %} 
{% if audience == "internal" %}|| `TAGS` | Service tag. 

Contains tags for the image. Values are extracted from frequency descriptions. | No attributes. ||{% endif %}
{% if audience == "internal" %}|| `_MetaSearcherHostname` | Service tag. 

Addresses of servers for upper-level metasearch and the image index. | No attributes. ||{% endif %}  
{% if audience == "internal" %}|| `_MimeType` | Service tag. 

The code of the document's MIME type and related information. | No attributes. ||{% endif %}
|| `_Name_ih` | The domain of the main site for the group of images. |	No attributes. ||
|| `_PassageAttrs` | Set of image attributes (size of duplicates, file format, image address, "foreign" flag, and so on). |	No attributes. ||
{% if audience == "internal" %}|| `_SearcherHostname` | Service tag. Name of the base search containing information about the image. | No attributes. ||{% endif %} 
|| `ih` | ID of the main site where the image is located. |	No attributes. ||
|#

> The `image-properties` grouping tag. Contains information about image properties that should be passed to search result output. No attributes.

#|
|| **Tag** | **Description** | **Attributes** ||
|| `id` | ID of the preview-size image copy (thumbnail). | No attributes. ||
|| `shard` | Number of the shard containing information about the image. | No attributes. ||
|| `thumbnail-width` | 	Width of the thumbnail image, in pixels. | No attributes. ||
|| `thumbnail-height` | Height of the thumbnail image, in pixels. | No attributes. ||
|| `thumbnail-link` | The address where the thumbnail image is available. | No attributes. ||
|| `original-width` {#original-width} | Width of the original image. | No attributes. ||
|| `original-height` {#original-height} | Height of the original image. | No attributes. ||
|| `html-link` {#html-link} | Address of the page where the image is published. | No attributes. ||
|| `image-link` {#image-link} | The address where the image is available. | No attributes. ||
|| `file-size` {#file-size} | Image size, in bytes. | No attributes. ||
|| `mime-type` {#mime-type} | Image format (JPG, GIF, etc.). | No attributes. ||
|#

> The `image-duplicates` grouping tag. Contains information about image duplicates. Information about each duplicate is put in the `image-properties` grouping tag.
>
> Each `image-properties` grouping tag contains the following tags with information about duplicates:
> - [original-width](#original-width)
> - [original-height](#original-height)
> - [html-link](#html-link)
> - [image-link](#image-link)
> - [file-size](#file-size)
> - [mime-type](#mime-type)
> 
> No attributes.

> The `image-duplicates-fitsize` grouping tag. Contains information about full-size duplicates of the image. Information about each duplicate is put in the `image-properties` grouping tag.
> 
> Each `image-properties` grouping tag contains the following tags with information about duplicates:
> - [original-width](#original-width)
> - [original-height](#original-height)
> - [html-link](#html-link)
> - [image-link](#image-link)
> - [file-size](#file-size)
> - [mime-type](#mime-type)
> 
> No attributes.

> The `image-duplicates-preview` tag. Contains information about preview-sized duplicates of the image. Information about each duplicate is put in the `image-properties` grouping tag.
> 
> Each `image-properties` grouping tag contains the following tags with information about duplicates:
> - [original-width](#original-width)
> - [original-height](#original-height)
> - [html-link](#html-link)
> - [image-link](#image-link)
> - [file-size](#file-size)
> - [mime-type](#mime-type)
> 
> No attributes.