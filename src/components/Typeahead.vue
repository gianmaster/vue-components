<template>
    <div :class="typeaheadState">
        <div class="typeahead__toggle" ref="toggle" @mousedown.prevent="toggle">
            <input 
                type="text" 
                class="typeahead__search" 
                ref="search" 
                @focus="onFocus" 
                @blur="onBlur"
                @keydown.esc="onEsc"
                @keydown.down="onKeyDown"
                @keydown.up="onKeyUp"
                @keydown.enter="onKeyEnter"
                v-model="search">
            <span class="typeahead__text" ref="text" >{{ search==='' ? displayText : '' }}</span>
        </div>
        <ul class="typeahead__list" v-if="open">
            <li class="typeahead__item" v-for="(option, idx) in filteredOptions" :key="idx">
                <a class="typeahead__link" @mousedown.prevent="select(option)" :class="{'typeahead__active': idx === selectIndex}">{{ option.text }}</a>
            </li>
        </ul>
    </div>
</template>
<script>

    export default {
        name: 'typeahead',
        computed: {
            typeaheadState() {
                return this.open ? 'typeahead typeahead__open' : 'typeahead'
            },
            filteredOptions() {
                const exp = new RegExp(this.search, 'i')
                return this.options.filter(option => {
                    return (exp.test(option.text || exp.test(option.id)))
                })
            }
        },
        props: {
            options: {
                type: Array,
                default() {
                    return []
                }
            },
            value: {
                type: [String, Number],
                default: null
            }
        },
        data() {
            return {
                open: false,
                displayText: 'Que chucha buscas',
                search: '',
                selectIndex: 0
            }
        },
        methods: {
            toggle(e) {
                if (this.$refs.toggle === e.target || this.$refs.search === e.target || this.$refs.text === e.target) {
                    if (this.open) {
                        if (e.target !== this.$refs.search && e.target !== this.$refs.text) {
                            this.$refs.search.blur()
                        }
                    } else {
                        this.$refs.search.focus()
                    }
                }
            },
            select(option) {
                this.displayText = option.text
                this.$emit('input', option.id)
                this.$refs.search.blur()
                this.selectIndex = this.filteredOptions.indexOf(option)
            },
            onFocus() {
                this.open = true
            },
            onBlur() {
                this.open = false
                this.search = ''
            },
            onEsc() {
                this.$refs.search.blur()
            },
            onKeyDown() {
                if (this.filteredOptions.length - 1 > this.selectIndex) {
                    this.selectIndex++
                }
            },
            onKeyUp() {
                if (this.filteredOptions.length > 0 && this.selectIndex >= 0) {
                    this.selectIndex--
                }
            },
            onKeyEnter() {
                const option = this.filteredOptions[this.selectIndex]

                if (option) {
                    this.select(option)
                }
            }
        }
    }

</script>
<style type="text/css">

    .typeahead{
        border-radius: 5px;
        border: 1px solid #ccc;
        z-index: 1;
        position: relative;
        width: 100%;
        font-size: 14px;
    }

    .typeahead__open {
        border: 1px solid #41b883;
    }

    .typeahead__open .typeahead__text {
        color: #999;
        opacity: 0.4;
    }

    .typeahead__toggle {
        width: 100%;
        z-index: 1;
        position: relative;
    }

    .typeahead__search {
        position: absolute;
        top: 0;
        left: 0;
        line-height: 1em;
        font-size: 1em;
        padding: 10px;
        width: 100%;
        display: block;
        cursor: text;
        background: transparent;
        border: none;
        outline: none;
        z-index: 2;
    }

    .typeahead__text {
        min-height: 36px;
        font-size: 1em;
        line-height: 1em;
        padding: 10px;
        display: inline-block;
        position: relative;
        z-index: 3;
    }

    .typeahead__list {
        margin: 0;
        padding: 0;
    }

    .typeahead__item {
        display: block;
        border-top: 1px solid #f4f4f4;
    }

    .typeahead__link {
        display: block;
        padding: 10px;
        line-height: 1em;
        font-size: 1em;
        cursor: pointer;
    }

    .typeahead__active {
        background: #44B883;
        color: #fff;
    }
</style>