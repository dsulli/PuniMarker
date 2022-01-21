

<template>
  <div class="grid lg:grid-cols-2 md:grid-cols-1 sm:grid-cols-1 gap-4">

    <div class="text-5xl lg:mb-0 mb-4 leading-9 lg:border-r-2 border-gray-600" :class="{'text-green-400': percentage >= 100, 'text-yellow-400': percentage >= 75 &&  percentage < 100}">
      <div><span >{{ count }}</span> / <span>{{ mobData.req }}</span></div>
      <span class="text-2xl text-gray-600">{{ percentage }}%</span>
    </div>
    <div class="lg:pl-2">
      <input type="number" min="0" v-model="count" class="w-full">
      <div class="mt-4 grid grid-cols-2 gap-2">
        <button class="mark-button  text-lg tracking-wider uppercase py-1 px-4  border-t-2 rounded-full  bg-gradient-to-b text-gray-100 font-bold outline-none" @click="count++">+1</button>
        <button class="mark-button text-lg tracking-wider uppercase py-1 px-4  border-t-2 rounded-full  bg-gradient-to-b text-gray-100 font-bold outline-none" @click="count += mobData.available">+{{ mobData.available }}</button>
      </div>
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
      count: 0
    }
  },
  computed: {
    percentage() {
      return Math.round(this.count / this.mobData.req * 100);
    }
  }
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
