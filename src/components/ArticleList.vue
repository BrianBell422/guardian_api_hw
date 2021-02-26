<template>
  <ul>
      <h2>Current Articles</h2>
      <list-item v-for="(article, index) in articles" :article="article" :key="index"></list-item>
  </ul>
</template>

<script>

import ListItem from './ListItem.vue'

export default {
    name: 'article-list',
    props:  ['articles'],
    components: {
        "list-item": ListItem
    }
}
</script>

<style>

</style>