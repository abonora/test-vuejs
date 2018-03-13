<template>
  <div class="hello">
    <div v-for="post in posts">
      <a :href="post.link" target="_blank"><img :src="post._embedded['wp:featuredmedia'][0].media_details.sizes.medium_large.source_url" :title="post.title.rendered" :alt="post.title.rendered" /></a>
      <a :href="post.link" target="_blank" v-html="post.title.rendered"></a>
      <p v-html="moment(post.date).format('dddd, MMMM DD, YYYY')"></p>
      <p>By: <a :href="post._embedded['author'][0].link" v-html="post._embedded['author'][0].name" target="_blank"></a></p>
      <p v-html="post.excerpt.rendered"></p>
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      posts: [],
      page: 1,
      count: 5
    }
  },
  methods: {
    moment: function(date){
      return moment(date);
    }
  },
  created: function(){
   this.$http.get('wp/v2/posts?page='+this.page+'&per_page='+this.count+'&_embed').then(response => {
    for(let post in response.data){
      this.posts.push(response.data[post]);
    }
   }, error => {
    console.log(error);
   });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.hello{
  clear: both;
  max-width: 1000px;
  margin: 0 auto;
  div{
    float: left;
    text-align: left;
    margin-bottom: 20px;
    img{
      float: left;
      margin-right: 10px;
      max-width: 300px;
    }
    p{
      margin: 0;
      // float: left;
      // display: block;
    }
  }
} 
</style>
