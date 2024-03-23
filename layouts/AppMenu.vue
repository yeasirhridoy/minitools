<script setup>
import { ref } from 'vue';
import AppMenuItem from './AppMenuItem.vue';

const model = ref([
    {
        label: 'Home',
        items: [{ label: 'Home', icon: 'pi pi-fw pi-home', to: '/' }]
    },
    {
        label: 'Counter',
        items: [
            {
                label: 'Word Counter',
                icon: 'pi pi-fw pi-pencil',
                to: '/word-counter'
            }
        ]
    },
    {
        label: 'Formatter',
        items: [
            {
                label: 'Time Formatter',
                icon: 'pi pi-fw pi-pencil',
                to: '/time-formatter'
            },
            {
                label: 'JSON Formatter',
                icon: 'pi pi-fw pi-pencil',
                to: '/json-formatter'
            }
            // {
            //   label: 'XML Formatter',
            //   icon: 'pi pi-fw pi-pencil',
            //   to: '/xml-formatter'
            // },
            // {
            //   label: 'SQL Formatter',
            //   icon: 'pi pi-fw pi-pencil',
            //   to: '/sql-formatter'
            // },
            // {
            //   label: 'HTML Formatter',
            //   icon: 'pi pi-fw pi-pencil',
            //   to: '/html-formatter'
            // },
            // {
            //   label: 'CSS Formatter',
            //   icon: 'pi pi-fw pi-pencil',
            //   to: '/css-formatter'
            // },
            // {
            //   label: 'Javascript Formatter',
            //   icon: 'pi pi-fw pi-pencil',
            //   to: '/javascript-formatter'
            // },
        ]
    },
    {
        label: 'Checker',
        items: [
            {
                label: 'Text Comparator',
                icon: 'pi pi-fw pi-pencil',
                to: '/text-comparator'
            },
            {
                label: 'Regex Checker',
                icon: 'pi pi-fw pi-pencil',
                to: '/regex-checker'
            }
        ]
    },
    {
        label: 'Generator',
        items: [
            {
                label: 'Text Generator',
                icon: 'pi pi-fw pi-pencil',
                to: '/text-generator'
            },
            {
                label: 'Password Generator',
                icon: 'pi pi-fw pi-pencil',
                to: '/password-generator'
            }
        ]
    },
    {
        label: 'Converter',
        items: [
            {
                label: 'Color Code Converter',
                icon: 'pi pi-fw pi-pencil',
                to: '/color-code-converter'
            },
            {
                label: 'Morse Code Converter',
                icon: 'pi pi-fw pi-pencil',
                to: '/morse-code-converter'
            },
            {
                label: 'URL Encoder Decoder',
                icon: 'pi pi-fw pi-pencil',
                to: '/url-encoder-decoder'
            },
            {
                label: 'Unit Converter',
                icon: 'pi pi-fw pi-pencil',
                to: '/unit-converter'
            },
            {
                label: 'Case Converter',
                icon: 'pi pi-fw pi-pencil',
                to: '/case-converter'
            },
            {
                label: 'Timezone Converter',
                icon: 'pi pi-fw pi-pencil',
                to: '/timezone-converter'
            }
        ]
    },
    {
        label: 'Calculator',
        items: [
            {
                label: 'Age Calculator',
                icon: 'pi pi-fw pi-pencil',
                to: '/age-calculator'
            },
            {
                label: 'BMI Calculator',
                icon: 'pi pi-fw pi-pencil',
                to: '/bmi-calculator'
            }
        ]
    },
    {
        label: 'Math',
        items: [
            {
                label: 'Math Generator',
                icon: 'pi pi-fw pi-pencil',
                to: '/math-generator'
            }
        ]
    }
]);
</script>

<template>
    <ul class="layout-menu">
        <template v-for="(item, i) in model" :key="item">
            <app-menu-item v-if="!item.separator" :item="item" :index="i"></app-menu-item>
            <li v-if="item.separator" class="menu-separator"></li>
        </template>
    </ul>
</template>

<style lang="scss" scoped></style>
