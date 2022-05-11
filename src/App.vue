<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import sData from './assets/data.json'
import  MobCounter from './components/MobCounter.vue'
export default {
  components: {
    MobCounter
  },
  data() {
    return {
      sData: sData
    }
  }
}
</script>

<template>
  <div class="">
    <div class="w-full bg-purple-300 text-gray-900 ">
      <div class="container mx-auto py-4 px-4 lg:px-0">
        <h2 class="md:text-4xl text-2xl font-bold">
          S Rank Spawn Kill Tracker
        </h2>
      </div>
    </div>
    <div class="w-full bg-purple-400 text-gray-900 hidden md:block">
      <div class="container mx-auto py-2 px-4 lg:px-0">
        <ul class="list-none">
          <li v-for="(sRank, index) in sData" :key="sRank.name" class="inline-block mr-3">
            <a :href="`#${sRank.name}`" class="font-bold text-lg text-purple-900 hover:text-pink-100">
            {{sRank.name}}
            </a>
            <span v-if="index !== sData.length - 1" class="pl-3 text-white">&bullet;</span>
          </li>
        </ul>
      </div>
    </div>
    <div class="container mx-auto w-full py-2 px-4 lg:px-0">
      <div class="lg:mt-6 mt-3 pb-3 py-2" v-for="sRank in sData" :key="sRank.name" :id="sRank.name">
        <h2 class="lg:text-3xl text-2xl uppercase   tracking-widest pb-2 border-b-2 border-gray-600"><span class="text-purple-300">{{ sRank.zone }}:</span> <span class="text-pink-300">{{ sRank.name }}</span></h2>
        <div class="grid xl:grid-cols-3 lg:grid-cols-2 md:grid-cols-1 sm:grid-cols-1 gap-4">
        <div class="my-4 bg-gray-900 py-4 px-6 rounded-xl" v-for="guy in sRank.mobs" :key="guy.name">
          <h3 class="font-bold text-gray-400 mb-4 text-2xl">{{ guy.name }}</h3>
          
          <div class="mb-2">
            <MobCounter :mob-data="guy"/>
          </div>
          <div>
            <span class="font-bold">Mobs Per Map</span>: {{ guy.available }}
          </div>
          <div class="mb-2">
            <span class="font-bold">Location</span>: {{ guy.locDesc }}
          </div>
          <img :src="guy.mapImg" class="w-full rounded-xl mb-2" />
          
        </div>
        </div>
      </div>
    </div>
    <div class="w-full bg-gray-700  ">
      <div class="container mx-auto py-4 px-4 lg:px-0 md:flex md:justify-between items-center">
         <div>
           <div>Made by Floon (2022)</div>
           <div>Contact: floon#0425 on Discord</div>
          </div>
         <div >
           <div>Map Images © SQUARE ENIX CO., LTD. All Rights Reserved.</div>
           Built with Vue3, Tailwind, and Netlify
          </div>
      </div>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Zen+Maru+Gothic:wght@400;500;700&display=swap');
body {
  @apply bg-gray-800 text-gray-300;
  font-family: 'Zen Maru Gothic', sans-serif;
}
</style>
