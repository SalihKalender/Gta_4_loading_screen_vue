<script setup>
  import { reactive, ref } from '@vue/reactivity'
  import { onBeforeMount, onMounted } from '@vue/runtime-core'
  import rockstar_games_logo from './assets/img/rockstar_games_logo.png'
  import rockstar_north_logo from './assets/img/rockstar_north_logo.png'
  import gta_4_logo from './assets/img/gta_4_logo.png'
  const intros = reactive([
    {intro_url: rockstar_games_logo},
    {intro_url: rockstar_north_logo},
    {intro_url: gta_4_logo},
  ])
  const is_showing = ref(-1)
  onMounted(() => {
    is_showing.value++;
  })
  setInterval(() => {
    // is_showing.value != 2 ? is_showing.value++ : null
    is_showing.value++
  },2400)
</script>
<template>
  <div class="container">
    <div v-for="(intro, index) in intros"  :key="index">
        <img :src="intro.intro_url" v-if="is_showing == index" :class="'intro intro_logo_' + index">
    </div>
    <button @click="is_showing++">
      <h2>TIKLA</h2>
    </button>
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
}
</style>
