<template>
  <div class="filmstrip">
    <!--{{mediaId}}-->
    <div class="carousel-wrapper">
      <flickity v-if="videos.length > 0" ref="flickity" :options="flickityOptions">
          <div class="carousel-cell" v-for="(video, key) in videos">
            <img :src="video.Images[0].Url" :title="video.Name" :alt="video.Name" />
            <p v-html="video.Name"></p>
          </div>
      </flickity>
    </div>
    <!-- <ul>
      <li v-for="(video, index) in videos">
        <img :src="video.Images[0].Url" :title="video.Name" :alt="video.Name" />
        <p v-html="video.Name"></p>
        <p v-html="index"></p>
      </li>
    </ul> -->
  </div>
  
</template>

<script>
import Flickity from 'vue-flickity'
export default {
  name: 'filmstrip',
  props: ['mediaId'],
  components: {
    Flickity
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      videos: [],
      page: 1,
      count: 5,
      propMediaId: this.mediaId,
      flickityOptions: {
        initialIndex: 0,
        pageDots: false,
        wrapAround: false,
        contain: true,
        cellAlign: 'left',
        setGallerySize: false,
        freeScroll: true
      }
    }
  },
  mounted: function(){
   this.getVideos();
  },
  methods: {
    getVideos(){
      this.$http.get('https://capi.9c9media.com/destinations/ctv_web/platforms/desktop/medias/'+this.propMediaId+'/contents?$include=[Authentication,Episode,Media.Id,Season,Genres,BroadcastDate,ItemsType,Items.ID,Images,Type,ShortDesc,Media.Name,Media.Images,Season,Episode,Genres,ContentPackages]&$inlinecount=true&$sort=BroadcastDate&$order=desc&$page=1&$top=9&images.type=thumbnail').then(response => {
        console.log(response);
        for(let video in response.data.Items){
          this.videos.push(response.data.Items[video]); 
        }
      }, error => {
        console.log(error);
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.filmstrip{
  float: left;
  clear: both;
  display: block;
  .carousel-wrapper{
    width: 1000px;
    height: 300px;
    outline: none;
  }
  .carousel-cell{
    width: 200px;
    height: 100%;
    img{
      width: 100%;
    }
  }
  ul{
    margin: 0;
    padding: 0;
    list-style: none;
    li{
      width: 210px;
      display: inline-block;
      float: left;
      img{
        max-width: 200px;
      }
    }
  }
}
</style>
