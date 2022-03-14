<!-- src/components/MyMap.vue -->
<!-- https://v3.cn.vuejs.org/guide/composition-api-provide-inject.html -->
<template>
  <MyMarker/>
  <button @click="updateLocation">父级组件更新 location</button>
</template>

<script>
  import { provide, reactive, readonly, ref } from 'vue'
  import MyMarker from './MyMarker.vue'

  export default {
    components: {
      MyMarker
    },
    setup() {
      const location = ref('North Pole')
      const geolocation = reactive({
        longitude: 90,
        latitude: 135
      })

      const updateLocation = () => {
        location.value = 'South Pole' + new Date().toLocaleString()
      }

      // provide('location', location)
      provide('location', readonly(location))  // 禁止在 inject 的地方 修改 location
      provide('geolocation', readonly(geolocation))
      provide('updateLocation', updateLocation)

      return {
        updateLocation
      }
    }
  }
</script>