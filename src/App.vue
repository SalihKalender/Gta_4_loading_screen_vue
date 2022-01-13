<script setup>
  import { reactive, ref } from '@vue/reactivity'
  import { onBeforeMount, onMounted } from '@vue/runtime-core'
  import rockstar_games_logo from './assets/img/rockstar_games_logo.png'
  import rockstar_north_logo from './assets/img/rockstar_north_logo.png'
  import gta_4_logo from './assets/img/gta_4_logo.png'
  import loading_audio_url from './assets/audio/gta_4_loading_screen_theme.mp3'

  import bg_1 from './assets/img/bg_1.jpg'
  import bg_2 from './assets/img/bg_2.jpg'
  import bg_3 from './assets/img/bg_3.jpg'
  import person_1 from './assets/img/person_1.png'
  import person_2 from './assets/img/person_2.png'
  import person_3 from './assets/img/person_3.png'

  const intros = reactive([
    {intro_url: rockstar_games_logo},
    {intro_url: rockstar_north_logo},
    {intro_url: gta_4_logo},
  ])

  const theme_items = reactive([
    {bg: bg_1, person: person_1},
    {bg: bg_2, person: person_2},
    {bg: bg_3, person: person_3},
  ])

  const is_showing_intro = ref(-1)
  const is_showing_theme = ref(-1)
  const audio_player = ref('')
  // audio_player.value.play()
  onMounted(() => {
    is_showing_intro.value++;
  })
  setInterval(() => {
    // is_showing_intro.value <= 2 ? is_showing_intro.value++ : null
    if(is_showing_intro.value <= 2) {
      is_showing_intro.value++
      if(is_showing_intro.value == 2) {
        setTimeout(() => {
          is_showing_theme.value = 0
        },3500)
      }
      return 
    }
  },3000)
  setTimeout(() => {
    setInterval(() => {
      is_showing_theme.value++
    },7000)
  },9000)  
</script>
<template>
  <div class="container">
    <div v-for="(intro, index) in intros"  :key="index">
        <img :src="intro.intro_url" v-if="is_showing_intro == index" :class="'intro intro_logo_' + index">
    </div>
    <!-- <audio :src="loading_audio_url" ref="audio_player"></audio> -->
    <div v-for="(item, index) in theme_items" :key="index">
      <img :src="item.bg" v-if="is_showing_theme == index" class="bg">
    </div>
  </div>  
</template>

<style lang="scss">
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .container {
    position: relative;
    overflow: hidden;
    width: 100vw;
    height: 100vh;
    background: #000000;  // cotainer'in bg'sini degistirmene gerek yok zaten tanıtımlardan sonra sadece bg_image'ler gelip onu kaplayacak
    .intro {
      position: absolute;
      height: auto;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
    }
    .intro_logo_2 {
      width: 600px;
      animation: logo_aniamtion 3s;
      @keyframes logo_aniamtion {
        0% {
          opacity: 0;
        }
        25% {
          opacity: 1;
        }
        70% {
          opacity: 1;
        }
        100% {
          opacity: 0;
        }
      }
    }
    .intro_logo_0, .intro_logo_1 {
      animation: intro_aniamtion 3s;
      @keyframes intro_aniamtion {
        0% {
          opacity: 0;
          width: 400px;
        }
        20% {
          opacity: 1;
        }
        70% {
          opacity: 1;
        }
        100% {
          width: 300px;
          opacity: 0;
        }
      }
    }
    .bg {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      -webkit-filter: grayscale(100%); /* Safari 6.0 - 9.0 */
      filter: grayscale(100%);
      animation: theme_bg_animation 7s linear;
      @keyframes theme_bg_animation {
        0% {
          transform: scale(1.20);
          opacity: 0;
        }
        30% {
          opacity: 1;
        }
        70% {
          opacity: 1;
        }
        100% {
          transform: scale(1);
          opacity: 0;
        }
      }
    }
  }
</style>
