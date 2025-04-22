# HTTP request parameters

A Yandex.Images search query is a request sent over the HTTP protocol to the URL `http://xmlsearch.yandex.<country-specific top-level domain>/xmlsearch?` . Search specifics are determined by the parameters that are appended to the end of the address after the ampersand symbol (`&`). The parameters can be passed in any order.

{% if audience == "internal" %}

The required set of parameters can differ, depending on which network the GET request comes from (the internal Yandex network, or an external one).

{% endif %}

The list of HTTP request parameters is provided in the table below.

### Mandatory parameters {#intservicesparms}

#|
|| **Parameter** | **Description**  | **Example** ||
|| `type` | Type of search.

When searching images, the value must be “pictures”. | `type=pictures` ||
|| `g` | Service parameter. Grouping properties.

Format: `1.ii.<number of results to return>.1.-1`.

The property “number of results to return” determines the maximum number of results that will be returned per HTTP request. Accepts a numerical value. {#numberofreturnedvalues} | `g=1.ii.20.1.-1` ||
|| `user` {#user} | The name of the user that the XML search is made for.

{% if audience == "internal" %}

Required when making a request from an external network.

{% endif %} | The following entry in the HTTP request corresponds to a partner who has the user name “abracadabra”:
`user=abracadabra` ||
|| `key` {#key} | The API key for Yandex.Images Search.

{% if audience == "internal" %}

Required when making a request from an external network.

{% endif %} | `key=<API key>` ||
|#

### Optional parameters {#optional-parameters}

#|
|| **Parameter** | **Description**  | **Example** ||
|| `fyandex` | Using the “Family search” filter when generating the search response.

Possible values:

- “0” — Family search enabled.
- “1” — Family search disabled.

If the parameter is omitted, the filter is not used. | `fyandex=1` ||
|| `icolor` | 	
Search for images containing the selected color.

Possible values:
- “gray” — Black-and-white.
- “color” — Color.
- “red”
- “orange”
- “yellow”
- “green”
- “cyan”
- “blue”
- “violet”
- “white”
- “black”

If the parameter is omitted, the filter is not used. | `icolor=gray` ||
|| `site` | Search for images from the specified web site.

If the parameter is omitted, the search is performed across all web sites in the search base. | `site=cactus.ru` ||
|| `type` | Type of image to find.

Possible values:

- “face” — Faces.
- “demotivator” — Demotivational posters.
- “photo” — Photographs.
- “clipart” — Pictures of objects against a uniform background.
- “lineart” — Outlines of objects.

If the parameter is omitted, the search is performed across all types of images. | `type=face` ||
|| `isize` | The desired size of image. Possible values:
- “enormous” — Images larger than 1600x1200.
- “large” — Images larger than 800х600.
- “medium” — Images in the range from 150x150 to 800x600.
- “small” — Images smaller than 150x150.
- “tiny” — Icons smaller than 32x32.
- “wallpaper” — Desktop-sized wallpaper.

If the parameter is omitted, the search is performed across images of all sizes. | `isize=large` ||
|| `itype` | The desired image format. Possible values:
- “jpg” — JPG images.
- “gif” — GIF images.
- “gifanim” — Animated GIF files.
- “png” — PNG images.

If the parameter is omitted, the search is performed across images in all formats. | `itype=gif` ||
|| `iorient` | Image orientation. Possible values:
- “horizontal”
- “vertical”
- “square”

If the parameter is omitted, the search is performed across images of any orientation. | `iorient=vertical` ||
|| `p` | Search results page. Defines the range of images to be returned (based on position in search output) when executing the HTTP request. Numbering starts from zero (the first page corresponds to the value “0”).

If the [number of results returned](#numberofreturnedvalues) is equal to “n”, and page “p” is requested, the search will produce those images that are positioned in the search output from `p*n+1` to `p*n+n` inclusively.

If the parameter is omitted, the search returns the first page from the search output for the given request (those images that are located in the positions from `1` to `n` inclusively). | `p=2` ||
|| `noreask` | Disables re-checking the request.

If set to “1”, returns results strictly as specified in the query, even if it contains a typo. | `noreask=1` ||
|| `fsdups` {#fsdups} | The number of full-size duplicates of an image to return.

If omitted, full-size duplicates are not searched for. | `fsdups=2` ||
|| `pvdups` {#pvdups} | 	
The number of preview-sized duplicates of an image to return.

If omitted, a single duplicate is returned. | `pvdups=2` ||
{% if audience == "internal" %}|| `i-m-a-hacker` | Internal parameter. Emulates an HTTP request from an external network. Only used when processing requests from the internal Yandex network.

For the value, it passes the IP address of a simulated user. The [user](#user) and [key](#key) parameters should also be set.

If the parameter value is omitted, the external network cannot be emulated. | `i-m-a-hacker=64.17.181.1` ||{% endif %}
|#

> The following HTTP request returns the first 20 image search results for the query “Mario Andretti” from the user “abracadabra” with the API key “08323.999ghfdsf”:
> 
> ```
> http://xmlsearch.yandex.com/xmlsearch?type=pictures&g=1.ii.20.1.-1&text=Mario Andretti&key=08323.999ghfdsf&user=abracadabra
> ```

