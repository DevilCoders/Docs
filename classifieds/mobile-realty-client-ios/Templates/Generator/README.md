# Generator

How to use:

$ cd /path/to/Realty/Templates
$ ./GeneratorExec


If you just want to edit a template-file you shouldn't rebuild a project
But if you want to add a new template-file then you **have to** support it in `switch fileName` and make release build 


How to make release build:

$ cd /path/to/Realty/Templates/Generator
$ swift build --configuration release
$ cp .build/release/Generator ../GeneratorExec


If you want to make changes - replace:
`let sourcePathString = Self.fileManager.currentDirectoryPath`
with
`let sourcePathString = "path/to/Realty/Templates"`

