<template>
 <v-card>
    <v-card-media
      transition="fade-transition"
      :src="cardInfo.thumbnailUrl"
      :height="cardThumbnail"
    >
    </v-card-media>
              <v-card-title primary-title>
                <v-layout wrap>
                <v-flex xs12>
            <div class="headline">{{reduceTitle}}</div>
            </v-flex>
            <v-layout row wrap justify-center>
              <v-flex d-flex style="padding-left:20px;" xs12>
            <span class="grey--text">Lorem ipsum dolor</span>
            </v-flex>
            </v-layout>
            </v-layout>
        </v-card-title>
      <v-layout wrap row mb-1>
        <v-flex xs12>
          <keep-alive>
         <component :is="componentId" v-show="showCustomComponent" transition="fade" transition-mode="out-in"></component>
        </keep-alive>
          </v-flex> 
      </v-layout>
             <v-bottom-nav
      shift
      :value="true"
      :active.sync="e2"
      :color="color"
    >
      <v-btn dark @click="closeOptions">
        <span>Close</span>
        <v-icon>close</v-icon>
      </v-btn>
      <v-btn dark @click="showAudioPlayer">
        <span>Music</span>
        <v-icon>music_note</v-icon>
      </v-btn>
      <v-btn dark @click="showText">
        <span>Read</span>
        <v-icon>subject</v-icon>
      </v-btn>
      <v-btn dark @click="showImage">
        <span>Image</span>
        <v-icon>image</v-icon>
      </v-btn>
    </v-bottom-nav>
      </v-card>
</template>

<script>
import audioPlayer from './audioPlayer'
import podcastText from './podcastText'
export default {
  components:{
    'podcast-audio-player':audioPlayer,
    'podcast-text':podcastText
  },
  props: ['cardInfo'],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      show:false,
      e2:3,
      componentId:'',
      showCustomComponent:false,
      cardThumbnail:'200px'
      }
    },
    methods:{
      onLoadPodcast(id){
        this.$router.push('/meetups/' + id)
      },
      showText(){
        if(!this.showCustomComponent)
          this.showCustomComponent = !this.showCustomComponent
          this.componentId = 'podcast-text'
          this.cardThumbnail = "200px"
      },
      showAudioPlayer(){
        if(!this.showCustomComponent)
          this.showCustomComponent = !this.showCustomComponent
        this.componentId = 'podcast-audio-player'
        this.cardThumbnail = "200px"
      },
      showImage(){
        if(this.showCustomComponent)
          this.showCustomComponent = !this.showCustomComponent
        this.cardThumbnail = "300px"
      },
      closeOptions(){
        this.showCustomComponent = !this.showCustomComponent
        this.cardThumbnail = "200px"
      }
    },
    computed: {
      color () {
        switch (this.e2) {
          case 0: return 'blue-grey'
          case 1: return 'teal'
          case 2: return 'brown'
          case 3: return 'indigo'
        }
      },
      reduceTitle(){
        return this.cardInfo.title.substring(0,10)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.fade-transition {
  transition: opacity 0.2s ease;
}

.fade-enter, .fade-leave {
  opacity: 0;
}

</style>
