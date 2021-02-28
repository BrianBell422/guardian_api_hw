<template>
  <div id="app">
  <header><h1>The Guardian</h1></header>
    <main>
      <div class="articles-summary-container">
        <section>
          <article-list :articles="articles" ></article-list>
        </section>
        <aside>
          <article-detail :article="selectedArticle" :favouriteArticles="favouriteArticles"></article-detail>
        </aside>
      </div>   
        <h3>Favourite Articles</h3>
        <favourite-articles :favouriteArticles="favouriteArticles" :selectedFavouriteArticle="selectedFavouriteArticle"></favourite-articles>
        <section>
          {{selectedFavouriteArticle}}
        </section>
    </main>
  </div>
</template>

<script>

import ArticleList from './components/ArticleList.vue';
import ArticleDetail from './components/ArticleDetail';
import FavouriteArticles from './components/FavouriteArticles.vue';

import { eventBus } from './main';

export default {
  name: 'App',
  data(){
    return {
      articles: [],
      selectedArticle: null,
      favouriteArticles: [],
      selectedFavouriteArticle: null,
    };
  },
  components: {
    "article-list": ArticleList,
    "article-detail": ArticleDetail,
    "favourite-articles": FavouriteArticles
  },
  mounted(){
    fetch('https://content.guardianapis.com/search?q=brexit&format=json&api-key=test')
    .then(res => res.json())
    .then(articles => this.articles = articles.response.results)

    eventBus.$on('article-selected', (article) => {
      this.selectedArticle = article
    })

    eventBus.$on('favourite-article', (article) => {
      this.favouriteArticles.push(article)
    })
    eventBus.$on('remove-favourite-article', (favouriteArticle) => {
      const index = this.favouriteArticles.findIndex((article) => {
        return article === favouriteArticle
      })
      this.favouriteArticles.splice(index, 1)
    })
    eventBus.$on('display-favourite-info', (favouriteArticle) => {
      // console.log(favouriteArticle.webUrl);
      this.selectedFavouriteArticle = favouriteArticle.webUrl
      
    })
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}

header {
  text-align: center;
  font-size: 35px;
}

.articles-summary-container { 
  display: grid;
  grid-template-columns: 1fr 1fr;
}
</style>
