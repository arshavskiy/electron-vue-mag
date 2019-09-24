<template>
  <main>

      <div class="main_box main_thumb" v-for="item in posts" :key="item.contentId" :style="{ backgroundImage: `url(${item.images.mainImage.url})` }">
          <div class="main_title">
              
              <router-link :to="{ name: 'article', params: { articleId: item.contentId }}">{{item.title}}</router-link>
          </div>
    
      </div>

  </main>

</template>

<script>

const fetch = require('node-fetch');


export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data() {
    return {
      posts: [],
      offset: 0
    }
  },
  created() {

    const hash =
      'key=e2yFGbr8SvG0mC5D6cRAEl3QIUnW4v9g&publisherId=thestartmagazine.com&userId=14558152';
    const headers = {
      'Content-Type': 'application/json; charset=utf-8',
      'accept': 'application/json; charset=utf-8',
      'Mode': 'no-cors'
    };

    const request = new Request('https://qaapi.thestartmagazine.com/mediaApi/v1.0/content?' + hash +
      '&language=en&limit=20&locale=en_US&category=news' +
      '&offset=' + this.offset, headers);

    fetch(request)
      .then(res => res.json())
      .then(res => {

        this.posts = res.content
      }).catch(err => {
        console.debug(err);
      });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  main {
      display: flex;
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: space-between;
  }

  .main_box {
      position: relative;
      width: 100vw;
      min-height: 20vh;
  }

  .main_thumb {
      width: calc(100vw - 10px);
      min-height: 20vh;
      background: #ddd;
      height: 220px;
      background-size: cover;
      background-position: top center;
      margin: 5px;
  }

  @media (min-width: 550px){
    .main_thumb{
      width: 48%;
      min-width: 150px;
    }
  }

  @media (min-width: 780px){
    .main_thumb{
      width: 32%;
      min-width: 150px;
    }
  }

  @media (min-width: 1080px){
    .main_thumb{
      width: 24%;
      min-width: 150px;
    }
  }

   @media (min-width: 1480px){
    .main_thumb{
      width: 15%;
      min-width: 150px;
    }
  }

    @media (max-width: 420px){
    .main_thumb{
      min-width: 350px;
    }
  }
  
  .main_title {
      background: linear-gradient(to top, black, transparent);
      position: absolute;
      bottom: 0;
      color: #fff;
      font-size: 1rem;
      padding: 15px 20px;
  }
</style>
