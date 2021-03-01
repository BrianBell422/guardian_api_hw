<template>
  <section>
    <ul>
      <li class="li-container" v-for="favouriteArticle in favouriteArticles">{{favouriteArticle.webTitle}} 
        <button class="green-button" v-on:click="displayFavouriteInfo(favouriteArticle)">Show full article</button> 
        <button class="red-button" v-on:click="removeFromFavourites(favouriteArticle)">Remove from favourites</button>
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
.green-button {
	background-color:#77b55a;
	border-radius:4px;
	border:1px solid #4b8f29;
	display:inline-block;
	cursor:pointer;
	color:rgb(16, 75, 236);
	font-size:13px;
	font-weight:bold;
	padding:6px 12px;
	text-decoration:none;
}

.red-button {
	background-color:#e4685d;
	border-radius:4px;
	border:1px solid #b23e35;
	display:inline-block;
	cursor:pointer;
	color:rgb(31, 82, 224);
	font-size:13px;
	font-weight:bold;
	padding:6px 12px;
	text-decoration:none;
}

.li-container {
  padding-top: 20px;
  display: grid;
  grid-template-columns: 5fr 1fr 1fr;
  grid-gap: 6px;
}
</style>