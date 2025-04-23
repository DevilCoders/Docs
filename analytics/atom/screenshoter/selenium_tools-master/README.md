### Description
`selenium_serp_screenshooter.py` makes screenshot for each url in `urls.txt` and place it to `out/` folder (`out/` folder is under gitignore). 

###Usage
- Goes to some tachka™ `scp const@const.haze.yandex.net://home/const/selenium/out/* .` and checkout this amazing repo and `cd` to it
- Create folders `out` and `errors` (they are under gitginore)
- Add urls ro `urls.txt`
- Change `ELEMENT_CLASS_NAME_SELECTOR` in `selenium_serp_screenshooter.py`. Script will use this selector to find element and make screenshoot (by default script uses distribution wizard's selector `z-default-search`)
- (optional) Change `desired_capabilities` in `selenium_serp_screenshooter.py` to select specific browser in selenium grid
- Run `python selenium_serp_screenshooter.py`
- Screenshot goes to `out` folder (one screenshoot for each url)
- If no element than screenshoot of whole page goes to `error` folder

###Requirements
- python's `selenium` library 
- python's `pillow` (you could install like this `pip install pillow`) 
