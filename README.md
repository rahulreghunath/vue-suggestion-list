<p align="center">

# vue-suggestion-list


##### Simple to use, mobile-friendly suggestion list using native html5 datalist



### Install

```bash
npm install vue-suggestion-list --save
```

### How to use

Include plugin in your project.

```javascript
import SuggestionList from 'vue-suggestion-list';

/*
 Use as global component 
 */
Vue.use(SuggestionList);

/*
 Or as local component
 */
const vue = new Vue({
    components:{
        SuggestionList
    }
});

```
---
Create list:

```vue
<suggestion-list :items="items" v-model="item"></suggestion-list>
```
Items must be an array of objects in the below format

```javascript
[
    {text: 'First', value: 1},
    {text: 'Two', value: 2},
    {text: 'Three', value: 3}
]
```
---

**Note:** Suggestion input box is given with two classes, ```form-control```,```vue-suggestion-input``` and
suggestion datalist is given with a default class of ```vue-suggestion-list```. So that you can applay custom styles on ```vue-suggestion-input``` and ```vue-suggestion-list``` classes.

### Properties

| Name      | Required | Type          | Default     | Description |
| ---       | ---      | ---           | ---         | ---         |
| items      | true  | Array |             | List items in the format ```[{value:'value',text:'text'}]``` |


Example:
```vue
<template>
  <list :items="items" v-model="value"></list>
</template>
<script>
export default {
  name: 'ExampleList',
  data () {
        return {
            value: '2',
            items: [
                {text: 'First', value: 1},
                {text: 'Two', value: 2},
                {text: 'Three', value: 3}
            ]
        }   
  },
 
}
</script>
```