<template>
    <div id="app">
        <div class="col-md-3">
            <div class="form-group">
                <list :items="items" v-model="value"></list>
            </div>
        </div>
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
                    {text: 'First', value: 1},
                    {text: 'Two', value: 2},
                    {text: 'Three', value: 3}
                ]
            }
        }
    }
</script>

<style>

</style>
