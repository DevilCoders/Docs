#### Parameters and arguments

CLI tool takes three config files: Services config, Parameters and Arguments. Services config is a common MPro config file. Parameters file consists of algorithm setting values: road buffer width, minimal weight of resulting hypothesis, signals loading buffer of the region and cell size for splitting the region. Arguments file contains task-specific information: bounding box of the region, range of dates for loading gps signals and limit for the number of signals to be processed. Parameters and Arguments files are protobuf files in text format.
