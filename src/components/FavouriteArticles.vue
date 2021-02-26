<template>
  <ul>
      <li v-for="favouriteArticle in favouriteArticles">{{favouriteArticle.webTitle}}</li>
  </ul>
</template>

<script>
import { eventBus } from '../main.js'

export default {
    name: 'favourite-articles',
    props: ['favouriteArticles']
}
</script>

<style>

</style>