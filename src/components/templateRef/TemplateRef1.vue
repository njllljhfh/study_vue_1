<template>
  <slot name="name1"></slot>
  <div ref="root">This is a root element</div>
</template>

<script>
  // 官网：https://v3.cn.vuejs.org/guide/composition-api-template-refs.html
  /*
    这里我们在渲染上下文中暴露 root，并通过 ref="root"，将其绑定到 div 作为其 ref。
    在虚拟 DOM 补丁算法中，如果 VNode 的 ref 键对应于渲染上下文中的 ref，则 VNode 的相应元素或组件实例将被分配给该 ref 的值。
    这是在虚拟 DOM 挂载/打补丁过程中执行的，因此模板引用只会在初始渲染之后获得赋值。

    作为模板使用的 ref 的行为与任何其他 ref 一样：它们是响应式的，可以传递到 (或从中返回) 复合函数中。
  */
  import { ref, onMounted } from 'vue'

  export default {
    setup() {
      const root = ref(null)

      onMounted(() => {
        // DOM 元素将在初始渲染后分配给 ref
        console.log(root.value) // <div>This is a root element</div>
        console.log(root.value.innerHTML) // This is a root element
      })

      return {
        root
      }
    }
  }
</script>