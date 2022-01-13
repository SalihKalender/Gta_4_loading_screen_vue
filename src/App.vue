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
    {bg: bg_1, person: person_1, position: Math.floor(Math.random() * 40) + 21},
    {bg: bg_2, person: person_2, position: Math.floor(Math.random() * 40) + 21},
    {bg: bg_3, person: person_3, position: Math.floor(Math.random() * 40) + 21},
  ])

  const is_showing_intro = ref(-1)
  const is_showing_theme = ref(-1)
  const audio_player = ref('')
  onMounted(() => {
    // is_showing_intro.value++;
  })
  const start_playing = () => {
    audio_player.value.volume = 1;
    is_showing_intro.value = -1;
    is_showing_theme.value = -1
    audio_player.value.play()
    setTimeout(() => {
      console.log(1)
      is_showing_intro.value++
      setInterval(() => {
        if(is_showing_intro.value < 1) {
          is_showing_intro.value++
        }
      },3000)
      setTimeout(() => {
        is_showing_intro.value++
        setInterval(() => {
          if(is_showing_intro.value <= 4) {
            is_showing_intro.value++
          }
        },7000)
      },6000)
      setTimeout(() => {
        is_showing_theme.value++
        setInterval(() => {
          is_showing_theme.value++
        },8500)
      },13500)  // intro 2 4000 s animation and 500ms wait
    },1500)
  }  
</script>
<template>
  <div class="container">
    <div v-for="(intro, index) in intros"  :key="index">
        <img :src="intro.intro_url" v-if="is_showing_intro == index" :class="'intro intro_logo_' + index">
    </div>
    <audio :src="loading_audio_url" ref="audio_player"></audio>
    <div v-for="(item, index) in theme_items" :key="index">
      <img :src="item.bg" v-if="is_showing_theme == index" class="bg">
      <img :src="item.person" v-if="is_showing_theme == index" class="person" :style="'left:' + item.position + '%'">
    </div>
    <button type="button" id="play_button" @click="start_playing">Play</button>
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
    #play_button {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%,-50%);
      padding: 15px 40px;
      font-size: 20px;
      font-weight: bold;
      background-color: #ffab00;
      color: #002d73;
      border: 2px solid #fff;
      border-radius: 10px;
      outline: none;
      transition: all .5s;
      &:hover {
        cursor: pointer;
        background-color: #002d73;
        color: #ffab00;
        transition: all .5s;
      }
    }
    .intro {
      position: absolute;
      height: auto;
      top: 50%;
      left: 50%;
      transform: translate(-50%,-50%);
      width: 300px;
    }
    .intro_logo_2 {
      width: 600px;
      animation: logo_aniamtion 7s;
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
      width: 0;
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
      animation: theme_bg_animation 8.5s linear;
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
    .person {
      position: absolute;
      bottom: 0;
      // left: 25%;   // Math.floor(Math.random() * 80) + 21;
      width: 25%;
      height: auto;
      animation: theme_person_animation 8.5s linear;
      @keyframes theme_person_animation {
        0% {
          transform: scale(1);
          opacity: 0;
        }
        10% {
          opacity: 1;
        }
        85% {
          opacity: 1;
        }
        100% {
          transform: scale(1.15);
          opacity: 0;
        }
      }
    }
  }
</style>