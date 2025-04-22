# Lego
Папка с проектами команды Лего. Тут живут вспомогательные скрипты для сборки и публикации пакетов и также все что связано с библиотекой islands.

<a name="structure"></a>
### Файловая структура

После переезда в Монорепозиторий файловая структура проектов Лего сильно видеизменилась

1. Из-за сильной связанности пакетов написанных на i-bem все что касается реализации islands на i-bem уехало в ```projects/lego/```, в частности это все что лежало в корне + некоторые [контрибы](#what-contribs)

2. Папка ```packages/``` из корня репозитория islands переехала в ```projects/lego/packages/```, а именно

_dist-generator  
_hermione-filenames  
_npm-scripts   
_palmsync-validate   
_prepare-publish   
_readme-md   
_specs-consistency   
ajax   
ci-helpers   
colors-inspector   
contribs-readme-generator   
counter   
detect-scripts   
doc-linter   
ensure-react-naming   
gap   
hedwig 
i-bem-react  
i-ua  
iframe-loader  
iver  
jest-bem-helpers  
lego-configs  
lego-dist-ts-generator  
pd-expanseur  
postcss-tone-vars  
rita-skeeter  
rpc  
selective  
selective-packages  
services  
slack-notifier-cli  
starter  
storybook-showcase  
tableau  
test-test  
tone-generator  
tools  
ts-docgen  
y-cookies  
yandex-font  

<a name="what-contribs"></a>

3. Все из папки ```contribs/``` переехало 

cookie-confirm  -> ```projects/lego/packages/```  
edu-components  -> ```packages/```  
favorites  -> ```packages/```  
global-notifications ->  ```services/```  
guidelines -> ```packages/```  
i-bem  -> ```projects/lego/packages/```  
islands  -> ```projects/lego/packages/```  
islands-deprecated -> ```projects/lego/packages/```  
lang-detector -> ```packages/```  
lego-components -> ```packages/```  
light-popup -> ```projects/lego/packages/```  
likes -> ```projects/lego/packages/```  
meccano -> ```projects/lego/packages/```  
messenger -> ```projects/lego/packages/```  
notifier -> ```projects/lego/packages/```  
pusher -> ```projects/lego/packages/```  
search-suggest -> ```projects/lego/packages/```   
serp-components -> ```packages/```  
serp-header -> ```packages/```  
suggest2 -> ```projects/lego/packages/```  
tools-suggest -> ```packages/```  
vendor-graphics -> ```packages/```  
video-components -> ```packages/```  
yaplus -> ```packages/```  
