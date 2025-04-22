### Format filter
**FilterImageFormatForImagesSearch**
This format filter is using to filter images mime types supported by images search service such as JPG, PNG etc.

**IsImageFormat**
This format filter is using to filter images mime types we could process with ImageMagick library.

### Format loader
**TAnyImageFormatLoader**
Load image from blob, blob format is recognized and filtered using IsImageFormat filter descibed above.
cv::Mat, mimetype and image attributes loaded for image is avalable.

### New format support
**To add new format support you should:**
1. Make sure arcadia contrib ImageMagick version supports new format.
2. Extend library/cpp/mime with new mime type for format, including format detecting procedure.
3.1. Extend IsImageFormat filter if you want to be able load new format blobs using TAnyImageFormatLoader.
3.2. Extend tests suite with new format samples, check tests, canonize tests.
4. Extend FilterImageFormatForImagesSearch with new mime type for format if you want new format to go through images search image pipeline.

