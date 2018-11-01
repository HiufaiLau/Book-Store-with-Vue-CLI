<template>
  <div class="home">
    <News v-for="(news, index) in newsArray" v-bind:key="index" :newsObj="news"/>

  </div>
</template>

<script>
// @ is an alias to /src
import News from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    News
  },
  data(){
    return {
      newsArray: [
        {title:"hello weather", tag:"weather", desc:"today is raning acid"},
        {title:"Nice time to go to London", tag:"Travel", desc:"this days are good to travel there"},
        {title:"Find a job in Berlin today", tag:"Business", desc:"if you are good come here"}
      ]
    }
  }
}
</script>
