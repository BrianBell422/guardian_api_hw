<template>
  <li v-on:click="handleClick">{{article.webTitle}}</li>
</template>

<script>
import { eventBus } from '../main'
export default {
    name: 'list-item',
    props: ['article'],
    methods: {
      handleClick(){
        eventBus.$emit('article-selected', this.article)
      }
    }
}
</script>

<style>

</style>