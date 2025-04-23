# Feature Position annotator

`annotator` tool creates easyview files for feature position annotation. It
takes file with space separated source ids and dates as input
(`rides_with_dates` for example).

## Usage

To start annotating, or viewing rides:
- Create easyview files with `./generate-easyview --help` (see help for arguments)
- Run easyview `cat generated_easyview_file | easyview --html=index.html`
- Run server (if you want to annotate) `python server.py --help` (flask dependency)

## Example

Dots with green outline are features, dots with red outline are track points.
Color of a dot depicts time: blue (start of the route) to yellow (end of the route)

<img src="https://jing.yandex-team.ru/files/irubachev/easyview_example1.png" width="200">
<img src="https://jing.yandex-team.ru/files/irubachev/easyview_example2.png" width="200">
<img src="https://jing.yandex-team.ru/files/irubachev/easyview_example3.png" width="200">


