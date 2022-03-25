<template>
  <!-- 这里的 el 是自定义的变量名，指的是所在的 div标签对象. -->
  <div v-for="(item, i) in list" :ref="el => { if (el) divs[i] = el }">
    <span :ref="el => { if (el) spans[i] = el }">{{ item }}</span>
    <button @click="updateDivInnerHtml(i)">修改div标签内部的值</button>
  </div>
</template>

<script>
  import { ref, reactive, onBeforeUpdate, onUpdated } from 'vue'

  export default {
    setup() {
      const list = reactive([1, 2, 3])
      const divs = ref([])
      const spans = ref([])

      // 确保在每次更新之前重置ref
      onBeforeUpdate(() => {
        // console.log('onBeforeUpdate')
        divs.value = []
        spans.value = []
      })

      onUpdated(() => {
        console.log('onUpdated')
        // console.log('span.innerHTML =', divs.value[0].getElementsByTagName('span')[0].innerHTML)
        console.log('spans 中的内容 =', spans.value[0].innerHTML) // 这里获取到的是更新前的内容
      })

      // 修改div标签内部的值
      function updateDivInnerHtml(index) {
        list[index] = new Date().toLocaleString() + '---xxxx'
        console.log('divs.value =', divs.value)
        // console.log('span.innerHTML =', divs.value[0].getElementsByTagName('span')[0].innerHTML)
        console.log('spans 中的内容 =', spans.value[index].innerHTML) // 这里获取到的是更新后的内容
      }

      return {
        list,
        divs,
        spans,  // 这里不return的话，template 中无法使用 spans 变量
        updateDivInnerHtml
      }
    }
  }
</script>