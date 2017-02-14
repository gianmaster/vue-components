<template>
    <div class="typeahead">
        <div class="typeahead__toggle">
            <input type="text" class="tepeahead__search" placeholder="Input some text" ref="search">
            <span class="typeahead__text" ref="text">Some text</span>
        </div>
        <ul class="typeahead__list">
            <li class="typeahead__item">
                <a class="typeahead__link">Item 1</a>
            </li>
            <li class="typeahead__item">
                <a class="typeahead__link">Item 2</a>
            </li>
            <li class="typeahead__item">
                <a class="typeahead__link">Item 3</a>
            </li>
        </ul>
    </div>
</template>
<script>

    export default {
        name: 'typeahead',
        data() {
            return {
                inputText: ''
            }
        }
    }

</script>
