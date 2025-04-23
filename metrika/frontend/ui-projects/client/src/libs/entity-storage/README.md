# Entity storage library

Решение, позволяющее кэшировать Entities в Redux Store, включает в себя:
* redux slice, определяющий набор actions/reducers для управления состоянием entities cache
* набор selectors для доступа к entity и entities list
* EntityRepository, предоставляющий API для запросов, инвалидации, удаления entity и entities list 
