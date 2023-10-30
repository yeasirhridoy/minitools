<script setup>
import {ref} from 'vue';
import AppMenuItem from './AppMenuItem.vue';

const model = ref([
  {
    label: 'Home',
    items: [{label: 'Home', icon: 'pi pi-fw pi-home', to: '/'}]
  },
  {
    label: 'Text',
    items: [
      {
        label: 'Word Counter',
        icon: 'pi pi-fw pi-pencil',
        to: '/word-counter'
      },
      {
        label: 'Color Code Converter',
        icon: 'pi pi-fw pi-pencil',
        to: '/color-code-converter'
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
