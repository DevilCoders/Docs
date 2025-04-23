# Admin Front TODO list

## General

- [X] add sidebar with navigation
- [X] remove PUBLIC_URL env var and switch to `homepage: "."` in `package.json`
- [X] add common notification engine

## Components

- [x] implement own wrappers around basic antd components to remove tight coupling to UI library

### FilterForm
- [ ] add proper validation to entries
- [ ] add an ability to insert suffix/prefix to entry
- [ ] make date entries to return Date or string instead of Moment
- [ ] add tooltips to entries showing labels

## Offers Page

- [X] implement offers filtering
- [X] use ~~Card~~ `List.Item` from antd for offer list items
- [X] use ~~ul/li elements~~ `List` from antd for list of offers
- [X] cancel fetching of offers if tab was changed during fetching process
- [X] move tabs to separate component
- [X] implement pagination
- [ ] add tips card header to show current active filters
- [X] take gearbox strings from static_create_data api
- [X] untie `activeTab` from `state` in offer page state. Changing the tab may fail, and we must
go back to the previous tab if request failed. `state` field must be updated only in case of 
request success 
- [ ] change offer data structure from array to object to optimize performance and simplify codebase
