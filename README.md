# VuePaginater - vue-paginater
[![npm (scoped)](https://img.shields.io/npm/v/vue-paginater.svg?style=flat-square)](https://www.npmjs.com/package/vue-paginater)
[![npm](https://img.shields.io/npm/dm/vue-paginater.svg?style=flat-square)](https://www.npmjs.com/package/vue-paginater)
[![MIT](https://img.shields.io/github/license/vahidhedayati/vue-paginater.svg?style=flat-square)](https://opensource.org/licenses/MIT)

## Installation via NPM

## First
Install via NPM 
```
npm i vue-paginater --save-dev
```
or
```
npm i  vue-paginater --save
```
## Second
Require in your project:
```
var VuePaginater = require('vue-paginater');
```
or ES6 syntax:
```js
import VuePaginater from 'vue-paginater'
```

# Third
You can register the component globally:
```
Vue.component('vue-paginater', VuePaginater)
                                                
```
Or locally in a single Vue component:
```
 components: { 'vue-paginater':VuePaginater},
```

#### All Available Props for vue-paginater

Prop | Type | Default | Description
--- | --- | --- | ---
maxVisibleButtons | Number | 3 | Amount of pages to show in pagination
total | Number| - | Total amount of results or iteration count
max| Number | 0 | If totalPages unset you must set how many entries you are showing per page i.e. 10 lines per page
enablePageListing| Boolean | true | show page numbers ?
enableFirstPage| Boolean | true | show first Button taking user to page 1?
enableLastPage| Boolean | true | show last Button taking user to  last page ?
firstLabel| String | First | Text to show as First  button
lastLabel| String | Last | Text to show as Last  button
nextLabel| String | Next | Text to show as Next button
previousLabel| String | Previous | Text to show as Previous  button
disabled| Boolean | false | Disable pagination

#### Events
Event | Description
--- | ---
@offset| Gives you back your current offset to go off and retrieve records from
@pagechanged | gives you current page number - but not really needed by you


## Usage

##### Example 1: Basic 
```html
<vue-paginater total="300" max="10" @offset="giveOffset"/>

```
```javascript
<script>
 import VuePaginater from 'vue-paginater'
 export default {
     components: {
         VuePaginater
     },
     methods: {
        giveOffset(offset) {
            console.log('currentOffet '+offset)
            //MyService.fetch('balh?offset='+offset)
        }
    }
 }
</script>
```

#### Changelog

#### v.1.0.0
- Working release built on webpack 4 - includes `vue-paginater` 

## Credits
### [Filipa Lacerda](https://alligator.io/vuejs/vue-pagination-component/)
This was the origins 
 
