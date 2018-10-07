<template>
    <div>
        <input class="form-control vue-suggestion-input" :list="'list'+_uid" ref="answerInput"
               v-model="suggestionInput"
               @change="suggestionChanged($event)"/>
        <datalist class="vue-suggestion-list" :id="'list'+_uid">
            <option v-for="list in lists" :key="list.value" :data-value="list.value">{{ list.text }}</option>
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
            value: {
                type: String,
            },
            items: {
                type: Array,
                default() {
                    return [{value: undefined, text: 'Nothing in the list'}];
                }
            }
        },
        data() {
            return {
                selected: this.value,
                lists: this.items,
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
                        this.$refs.answerInput.value = option.value;
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
                let list = e.target.getAttribute('list');
                let options = document.querySelectorAll('#' + list + ' option'),
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