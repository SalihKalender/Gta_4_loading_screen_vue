<script setup>
  import { reactive, ref } from '@vue/reactivity'
  import rockstar_games_logo from './assets/img/rockstar_games_logo.png'
  import rockstar_north_logo from './assets/img/rockstar_north_logo.png'
  import gta_4_logo from './assets/img/gta_4_logo.png'
  const intros = reactive([
    { 
      intro_url: rockstar_games_logo
    },
    { 
      intro_url: rockstar_north_logo   // Burası
    },
    { 
      intro_url: gta_4_logo   // Burası
    },
  ])
  const is_showing = ref(0)
  
</script>
<template>
  <div class="container">
    <div v-for="(intro, index) in intros"  :key="index">
      <transition :name="'intro_' + index" mode="out-in">
        <img :src="intro.intro_url" :id="'img_' + index"  v-if="is_showing == index">
      </transition>
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
    #img_0, #img_1, #img_2 {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 400px;
      height: auto;
    }
  }
  .intro_0-enter-from, .intro_1-enter-from {
    opacity: 0;
    width: 500px !important;
  }
  .intro_0-enter-to, .intro_1-enter-to {
    opacity: 1;
    width: 400px !important;
  }
  .intro_0-enter-active, .intro_1-enter-active, .intro_0-leave-active, .intro_1-leave-active {
    transition: all 2s;
  }
  .intro_1-enter-active {
    transition-delay: 2s;
  }
  .intro_0-leave-from, .intro_1-leave-from {
    opacity: 1;
    width: 400px !important;
  }
  .intro_0-leave-to, .intro_1-leave-to {
    opacity: 0;
    width: 300px !important;
  }
  .intro_2-enter-from {
    opacity: 0;
  }
  .intro_2-enter-to {
    opacity: 1;
  }
  .intro_2-enter-active{
    transition: opacity 2s linear;
    transition-delay: 2s;
  }
  .intro_2-leave-from {
    opacity: 1;
  }
  .intro_2-leave-to {
    opacity: 0;
  }
</style>
