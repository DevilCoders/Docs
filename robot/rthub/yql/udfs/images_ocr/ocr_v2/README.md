To prepare OcrData archive:

1) Checkout ${arcadia_test_data}/images/ocr/yimages
2) Build ${arcadia}/cv/imageproc/ocr/ocr_runner
3) Build ${arcadia}/cv/imageproc/ocr/tools/database_extraction/nirvana/get_single_config_data
4) Run:

${arcadia}/cv/imageproc/ocr/tools/database_extraction/nirvana/get_single_config_data/get_single_config_data ${arcadia} ${arcadia_tests_data}/images/ocr yimages/ocr.cfg ocrdata.tar

5) ya upload --ttl=inf ocrdata.tar
