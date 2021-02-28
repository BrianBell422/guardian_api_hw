<template>
  <section>
    <ul>
      <li v-for="favouriteArticle in favouriteArticles">{{favouriteArticle.webTitle}} 
        <button v-on:click="displayFavouriteInfo(favouriteArticle)">Show full article</button> 
        <button v-on:click="removeFromFavourites(favouriteArticle)">Remove from favourites</button>
      </li>
    </ul>
  </section>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'favourite-articles',
  props: ['favouriteArticles', 'selectedFavouriteArticle'],
  methods: {
    removeFromFavourites: function(favouriteArticle){
      eventBus.$emit('remove-favourite-article', favouriteArticle)
    },
    displayFavouriteInfo: function(favouriteArticle){
      eventBus.$emit('display-favourite-info', favouriteArticle)
    },
  }  
}
</script>

<style>

</style>