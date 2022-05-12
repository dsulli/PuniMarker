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
        <h2 class="lg:text-3xl text-2xl uppercase   tracking-widest pb-2 border-b-2 border-gray-600">
          <span class="text-purple-300">{{ sRank.zone }}:</span> 
          <span class="text-pink-300">{{ sRank.name }}</span>
        </h2>
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

    <div class="container mx-auto w-full py-2 px-4 lg:px-0 mb-10">
        <h2 class="lg:text-3xl text-2xl uppercase   tracking-widest pb-2 border-b-2 border-gray-600">
          <span class="text-purple-300">About</span> 
        </h2>
        
        <div class="grid xl:grid-cols-3 lg:grid-cols-2 md:grid-cols-1 sm:grid-cols-1 gap-4">
          <div class="my-4 bg-gray-900 py-4 px-6 rounded-xl">
            <h3 class="font-bold text-gray-400 mb-4 text-2xl">How To Use</h3>
            
            <div class="mb-8">
              <ul class="list-disc pl-6">
                <li class="mb-4">
                  <div class="font-bold text-purple-300 inline-block">Incrementing The Count</div>
                  <p>
                    You can either increment by +1 or by lap via the giant purple buttons.
                  </p>
                </li>
                <li>
                  <div class="font-bold text-purple-300 inline-block">Changing The Lap Amount</div>
                  <p>
                    There is an input next to the label "Mobs Per Lap." Change the number in that input and the lap button will change automatically.
                  </p>
                </li>
              </ul>
            </div>

            <h3 class="font-bold text-gray-400 mb-4 text-2xl">Start The Spawn Attempt</h3>
            
            <div class="mb-4">
              <ul class="list-decimal pl-6">
                <li class="mb-4">
                  <div class="font-bold text-purple-300 inline-block">Check Faloop to see if the window is open.</div>
                  <p>
                    Check out your world's S rank windows at <a href="https://faloop.app/" target="_blank" class="font-bold text-purple-500 hover:text-pink-300">Faloop</a>.
                  </p>
                </li>
                <li class="mb-4">
                  <div class="font-bold text-purple-300">Head over to the location specified for one of the mobs.</div>
                </li>
                <li class="mb-4">
                  <div class="font-bold text-purple-300">Find a route and determine where the lap starts and ends.</div>
                </li>
                <li class="mb-4">
                  <div class="font-bold text-purple-300">Kill the mobs and increment the counter once you've finished a lap.</div>
                </li>
                <li class="mb-4">
                  <div class="font-bold text-purple-300">Repeat until you've fulfilled the spawn requirements.</div>
                  <p>If the attempt failed, it's nice to let others spawners know so they don't try too soon after.</p>
                </li>
              </ul>
            </div>
            
          </div>

          <div class="my-4 bg-gray-900 py-4 px-6 rounded-xl">
            <h3 class="font-bold text-gray-400 mb-4 text-2xl">Notes</h3>
            <div class="mb-8">
              <div class="font-bold text-purple-300">What is this for?</div>
              <p>
                Some S ranks have spawn conditions that require you to kill a certain amount of specific mobs. If the hidden timer is ready and you fulfil that requirement, it will spawn.
                Spawners want to know if their attempt at spawning an S rank failed. If the hidden timer is not ready and you fulfiled the kill requirement, you'll know that the S rank isn't ready to spawn and you can try again later.
              </p>
            </div>
            <div class="mb-8">
              <div class="font-bold text-purple-300">Why this and not ACT?</div>
              <p>
                Many spawners use ACT to automatically count how many of the same mob were killed. 
                The reason I made this tool was to account for mobs killed by people not in your party or vicinity. ACT might not pick up everything, so this tool lets you increment the count manually.
                There are also times where you pause your attempt to do something else.
                I have to mention that ACT technically violates the TOS, so use it at your own risk.
              </p>
            </div>
            <hr class="mb-8 border-gray-600"/>
            <div class="mb-4">
              <p>This tool is made independently by Floon and is not affiliated with any other development projects.</p>
            </div>
          </div>

          <div class="my-4 bg-gray-900 py-4 px-6 rounded-xl">
            <h3 class="font-bold text-gray-400 mb-4 text-2xl">Feedback</h3>
            <p>Right now the best way to contact is through the Aether Hunts Discord. If you're not on the Aether Data Center, try and find me from another FFXIV-related discord. My Discord name is Floon#0425.</p>
            <h3 class="font-bold text-gray-400 mb-4 text-2xl mt-8">Support Me</h3>
            <p>I do not make any money from this nor does it cost any money to run. Don't give me your money. Unless you want to <a href="https://www.etsy.com/shop/flareboostshop" target="_blank" class="font-bold text-purple-500 hover:text-pink-300">buy my fan merch.</a></p>
            <img :src="'./fat-cat.png'" class="w-full mb-2" />
          </div>
        </div>
    </div>

    <div class="w-full bg-gray-700  ">
      <div class="container mx-auto py-4 px-4 lg:px-0 md:flex md:justify-between items-center">
         <div>
           <div>Made by Floon (2022)</div>
          </div>
         <div >
           <div>Map Images © SQUARE ENIX CO., LTD. All Rights Reserved.</div>
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
