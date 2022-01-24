

<template>
  <div >
    <div class="grid lg:grid-cols-2 md:grid-cols-1 sm:grid-cols-1 gap-4">
    <div class="lg:pr-4 2xl:text-5xl text-4xl lg:mb-0 mb-4 leading-9 lg:border-r-2 border-gray-600 tracking-tighter" :class="{'text-green-400': percentage >= 100, 'text-yellow-400': percentage >= 75 &&  percentage < 100}">
      <div><span >{{ count }}</span> / <span>{{ mobData.req }}</span></div>
      <div class="relative pt-2 2xl:pb-0 pb-4">
        <div class="absolute bg-gray-200 rounded-full w-full h-4 mt-4 border-2 border-gray-100"></div>
        <div class="absolute  rounded-full h-4 mt-4 border-2 border-gray-100 bg-gradient-to-b" :class="{'from-gray-500 to-gray-400': percentage < 75, 'from-green-600 to-lime-500': percentage >= 100, 'from-yellow-500 to-yellow-300': percentage >= 75 &&  percentage < 100}" :style="progressBarStyle"></div>
      </div>
      <!-- <span class="text-2xl text-gray-600">{{ percentage }}%</span> -->
    </div>
    <div class="lg:pl-2">
      <input type="number" min="0" :max="parseInt(mobData.req)" v-model="count" class="w-full">
      <div class="mt-4 grid grid-cols-2 gap-2">
        <button class="mark-button  text-lg tracking-wider uppercase py-1 px-4  border-t-2 rounded-full  bg-gradient-to-b text-gray-100 font-bold outline-none" @click="count + 1 <= mobData.req ? count++ : mobData.req">+1</button>
        <button class="mark-button text-lg tracking-wider uppercase py-1 px-4  border-t-2 rounded-full  bg-gradient-to-b text-gray-100 font-bold outline-none" @click="incByLap">+{{ incrementer }}</button>
      </div>
    </div>
    </div>
    <div class="mt-4 flex w-full content-center items-center">
      <div class="text-xl mr-2 text-gray-400 font-bold">Mobs Per Lap:</div> <input type="number" min="2" :max="mobData.available" v-model="incrementer" class="w-16">
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'mobData'
  ],
  data() {
    return {
      msg: "hi",
      count: 0,
      incrementer: this.mobData.available
    }
  },
  computed: {
    percentage() {
      return Math.round(this.count / this.mobData.req * 100);
    },
    progressBarStyle() {
      let percent = this.percentage <= 100  ? this.percentage : 100;
      let display = this.percentage < 6 ? "none" : "inline-block";
      return {
        width: `${percent}%`,
        display: display
      };
    }
  },
  watch: {
    count(input) {
      if(input > this.mobData.req) {
        this.count = this.mobData.req;
      } else if(input < 0 || input == "") {
        this.count = 0;
      }
    },
    incrementer(input) {
      if(input > this.mobData.available) {
        this.incrementer = this.mobData.available;
      } else if(input < 0 || input == "") {
        this.incrementer = 2;
      }
    }
  },
  methods: {
    incByLap() {
      if(this.count + this.incrementer <= this.mobData.req) {
        this.count += this.incrementer;
      } else {
        this.count = this.mobData.req;
      }
    }
  }
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
