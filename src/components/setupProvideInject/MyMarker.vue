<!--src/components/MyMarker.vue -->
<template>
  <h1>{{ userLocation }}</h1>
  <button @click="updateUserLocation">组件更新 location</button>
  <p>longitude: {{ userGeolocation.longitude }}</p>
  <p>latitude: {{ userGeolocation.latitude }}</p>
</template>

<script>
  import { inject } from 'vue'

  export default {
    setup() {
      const userLocation = inject('location', 'The Universe')
      const userGeolocation = inject('geolocation')
      // 父级组件即使使用了 readonly，此 inject 的方法仍然可以执行
      const updateUserLocation = inject('updateLocation')

      // 父级组件若使用了 readonly 此方法会报错
      // const updateUserLocation = () => {
      //   userLocation.value = 'South Pole' + new Date().toLocaleString()
      // }

      return {
        userLocation,
        userGeolocation,
        updateUserLocation
      }
    }
  }
</script>

<style scoped>

</style>