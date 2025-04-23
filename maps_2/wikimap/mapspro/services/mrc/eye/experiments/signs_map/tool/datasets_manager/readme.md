Dataset manager:
  Action:
    1) download - download dataset from YT and save to JSON.
    2) upload - upload dataset from JSON to YT.

  Dataset type:
    1) images - dataset with images
    2) objects - dataset with detected objects on images
    3) matches - dataset with matches on pairs of features
    4) clusters - dataset with clusters of objects on images

  Attributes:
    --json - path to JSON file
    --table - path to YT table

  Examples:
    - Download images dataset from table '//home/images' to JSON file 'images.json'.
        dataset_manager download images --table //home/images --json images.json
    - Upload matches dataset from JSON file 'matches.json' to YT table '//home/matches'
        dataset_manager upload matches --json matches.json --table //home/matches
