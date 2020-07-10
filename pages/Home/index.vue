<template>
  <div class="home-page">
    <div class="banner">
      <div class="container">
        <h1 class="logo-font">conduit</h1>
        <p>A place to share your knowledge.</p>
      </div>
    </div>

    <div class="container page">
      <div class="row">
        <div class="col-md-9">
          <div class="feed-toggle">
            <ul class="nav nav-pills outline-active">
              <li class="nav-item">
                <a class="nav-link disabled" href @click.prevent="handleShowYourFeed">Your Feed</a>
              </li>
              <li class="nav-item">
                <a class="nav-link active" href @click.prevent="handleShowGlobalFeed">Global Feed</a>
              </li>
            </ul>
          </div>

          <div class="article-preview" v-for="item in articles" :key="item.slug">
            <div class="article-meta">
              <nuxt-link :to="`profile/${item.slug}`">
                <img :src="item.author.image" />
              </nuxt-link>
              <div class="info">
                <nuxt-link href class="author">{{item.author.username}}</nuxt-link>
                <span class="date">{{ item.updatedAt}}</span>
              </div>
              <button class="btn btn-outline-primary btn-sm pull-xs-right">
                <i class="ion-heart"></i> {{item.favoritesCount}}
              </button>
            </div>
            <a href class="preview-link">
              <h1>How to build webapps that scale</h1>
              <p>This is the description for the post.</p>
              <span>Read more...</span>
            </a>
          </div>

          <div class="article-preview">
            <div class="article-meta">
              <a href="profile.html">
                <img src="http://i.imgur.com/N4VcUeJ.jpg" />
              </a>
              <div class="info">
                <a href class="author">Albert Pai</a>
                <span class="date">January 20th</span>
              </div>
              <button class="btn btn-outline-primary btn-sm pull-xs-right">
                <i class="ion-heart"></i> 32
              </button>
            </div>
            <a href class="preview-link">
              <h1>The song you won't ever stop singing. No matter how hard you try.</h1>
              <p>This is the description for the post.</p>
              <span>Read more...</span>
            </a>
          </div>
        </div>

        <div class="col-md-3">
          <div class="sidebar">
            <p>Popular Tags</p>

            <div class="tag-list">
              <a href class="tag-pill tag-default">programming</a>
              <a href class="tag-pill tag-default">javascript</a>
              <a href class="tag-pill tag-default">emberjs</a>
              <a href class="tag-pill tag-default">angularjs</a>
              <a href class="tag-pill tag-default">react</a>
              <a href class="tag-pill tag-default">mean</a>
              <a href class="tag-pill tag-default">node</a>
              <a href class="tag-pill tag-default">rails</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import {GloablFeed, YourFeed} from '@/api/home'
export default {
name:'Home',
data(){
  return {
    article:[],
  }
},

methods: {
   async handleShowGlobalFeed(){
     const { comments } = await GloablFeed();
  },
 async handleShowYourFeed(){
     const { comments } = await YourFeed({});
  },
},

mounted(){
 const { article } = await ArticalList({
   limit: 20,
   offset: 0,
 });
}
}
</script>

<style>
</style>