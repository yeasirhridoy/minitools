<script setup>
import {ref} from 'vue';
import AppMenuItem from './AppMenuItem.vue';

const model = ref([
  {
    label: 'Home',
    items: [{label: 'Home', icon: 'pi pi-fw pi-home', to: '/'}]
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
      }
    ]
  },
  {
    label: 'Calculator',
    items: [
      {
        label: 'Birthday Calculator',
        icon: 'pi pi-fw pi-pencil',
        to: '/birthday-calculator'
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
