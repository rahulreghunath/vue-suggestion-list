<template>
    <div id="app">
        <list :items="items" v-model="value"></list>
    </div>
</template>

<script>
    import('bootstrap/dist/css/bootstrap.css');

    import List from '../SuggestionList/SuggestionList';

    export default {
        name: 'app',
        components: {List},
        data() {
            return {
                value: '2',
                items: [
                    {option: 'First', value: 1},
                    {option: 'Two', value: 2},
                    {option: 'Three', value: 3}
                ]
            }
        }
    }
</script>

<style>

</style>
