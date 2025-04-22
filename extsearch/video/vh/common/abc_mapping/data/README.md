After change abc_mapping.json should run:

ya make extsearch/video/vh/tools/make_from_whitelist && extsearch/video/vh/tools/make_from_whitelist/make_from_whitelist --output extsearch/video/vh/conf/from_whitelist


abc_mapping rules:
1. name match: abc{ID}{"ProductService"}[*]{"FrontendFrom"} || abc{ID}{"mapping_name"}[*]
2. regexp match: abc{ID}{"mapping_re"}[*]

from_whitelist rules:
if (!abc{ID}{"ProductService"}[*]{"from_whitelist_skip"})
    abc{ID}{"ProductService"}[*]{"FrontendFrom"}
+ from_whitelist_add[*]
