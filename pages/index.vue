<template>
  <div class="py-12 bg-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="lg:text-center">
        <NuxtLogo />
        <br />
        <h1
          class="text-3xl text-indigo-600 font-semibold tracking-wide uppercase"
        >
          NuxtJs
        </h1>
        <br />
        <button
          class="
            text-purple-500
            bg-transparent
            border border-solid border-purple-500
            hover:bg-purple-500 hover:text-white
            active:bg-purple-600
            font-bold
            uppercase
            text-xs
            px-4
            py-2
            outline-none
            focus:outline-none
            mb-1
            ease-linear
            transition-all
            duration-150
          "
          @click="loadData"
        >
          click
        </button>
        <div class="grid grid-cols-2 gap-4">
          <div
            v-if="loadedData.length"
            class="mt-4 max-w-2xl text-xl text-gray-500 lg:mx-auto"
          >
            <ul>
              <li
                v-for="dato of loadedData"
                :key="dato.index"
                class="ext-sm font-medium text-blue-600"
              >
                {{ dato.eyeColor }}
              </li>
            </ul>
          </div>
          <div class="mt-4 max-w-2xl text-xl text-gray-500 lg:mx-auto">
            <ul>
              <li
                v-for="dato of datos"
                :key="dato.index"
                class="ext-sm font-medium text-gray-900"
              >
                {{ dato.eyeColor }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  async asyncData({ $axios }) {
    const datos = await $axios.$get('http://stange.ar/resources/data.json')
    console.log(datos.length)
    // datos = datos.map((item) => item.eyeColor)
    return {
      datos,
    }
  },
  data() {
    return {
      loadedData: [],
    }
  },
  methods: {
    loadData() {
      axios.get('http://stange.ar/resources/data.json').then(
        function (response) {
          this.loadedData = response.data
        }.bind(this)
      )
      console.log(this.loadedData)
    },
  },
}
</script>
