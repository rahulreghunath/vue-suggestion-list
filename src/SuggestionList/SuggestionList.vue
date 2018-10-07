<template>
    <div>
        <input class="form-control vue-suggestion-input" list="suggestionList" id="answerInput"
               v-model="suggestionInput"
               @change="suggestionChanged($event)"/>
        <datalist class="vue-suggestion-list" id="suggestionList">
            <option v-for="item in items" :key="item.value" :data-value="item.value">{{ item.text }}</option>
        </datalist>
    </div>
</template>

<script>
    export default {
        name: "SuggestionList",
        model: {
            prop: 'value',
            event: 'change'
        },
        props: {
            value: String,
            items: Array
        },
        data() {
            return {
                selected: this.value,
                suggestionInput: ''
            }
        },
        watch: {
            selected() {
                this.$emit('change', this.selected);
            },
            suggestionInput() {
                if (this.suggestionInput === '') {
                    this.selected = '';
                }
            }
        },
        methods: {
            suggestionChanged(e) {
                if (this.selected !== '') {
                    let options = document.querySelectorAll('#suggestionList option');

                    for (let i = 0; i < options.length; i++) {
                        let option = options[i];
                        if (option.value === e.target.value) {
                            return;
                        }
                    }
                    this.initialValue();
                }
            },
            initialValue() {
                let options = document.querySelectorAll('#suggestionList option');

                for (let i = 0; i < options.length; i++) {
                    let option = options[i];
                    if (option.getAttribute('data-value') === this.selected) {
                        document.getElementById('answerInput').value = option.value;
                        break;
                    }
                }
            }
        },
        mounted() {
            if (this.selected.length) {
                this.initialValue();
            }
            document.querySelector('input[list]').addEventListener('input', (e) => {
                let options = document.querySelectorAll('#suggestionList option'),
                    inputValue = e.target.value;

                for (let i = 0; i < options.length; i++) {
                    let option = options[i];

                    if (option.innerText === inputValue) {
                        this.selected = option.getAttribute('data-value');
                        break;
                    }
                }
            });
        }
    }
</script>

<style scoped>

</style>