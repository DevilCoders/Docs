### binaries.sh
This script outputs paths to all binaries, which are required for stitching.
Ex.: ./binaries.sh

### ldd.sh
This script outputs paths to all libraries, which are required for stitching.
Useful to check that all binaries are present on a system and to inspect libraries.
Ex.: ./ldd.sh

### ldd-basename.sh
This script outputs all filenames of libraries, which are required for stitching.
Useful to change list of libraries in ../main.cpp.
Ex.: ./ldd-basename.sh

### upload.sh
This script:
* patches copies of all binaries and libraries to make them relocatable (can be run on YT)
* uploads them to Cypress path //home/maps/streetview/autostitcher/{ENV}/bin/
Ex.: ./upload.sh development
