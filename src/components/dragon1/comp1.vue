<template>
  <div>
    <span>{{ count }}</span>
    <button @click="count ++">Increment count</button>
    <button @click="nested.count.value ++">Nested Increment count</button>
  </div>
</template>

<script>
  /*测试响应式变量*/
  import { ref } from 'vue'

  export default {
    setup() {
      const count = ref(0)
      // const count = 0  // 改成这样，count就不是响应式的了
      return {
        count,

        nested: {
          count
        }
      }
    }
  }
</script>