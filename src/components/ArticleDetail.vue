<template>
  <div v-if="article" id="articleDetail">
    <h2>Selected Article Summary</h2>
    <h3>{{article.webTitle}}</h3>
    <section>
        <p><b>Category: </b>{{article.sectionName}}</p>
    </section> 
    <button class="green-button" v-if="!favouriteArticles.includes(article)" v-on:click="addToFavourites">Add to favourites</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
    name: 'article-detail',
    props: ['article', 'favouriteArticles'],
    methods: {
        addToFavourites: function(){
            eventBus.$emit('favourite-article', this.article)
        }
    }
}
</script>

<style>

</style>