<template>
  <div ref="root">This is a root element - 3</div>
</template>

<script>
  import { ref, watchEffect } from 'vue'

  export default {
    setup() {
      const root = ref(null)

      watchEffect(() => {
          console.log(root.value) // => <div>This is a root element</div>
        },
        {
          /*
          侦听模板引用的变更可以替代前面例子中演示使用的生命周期钩子。
          但与生命周期钩子的一个关键区别是，watch() 和 watchEffect() 在 DOM 挂载或更新之前运行回调函数，所以当侦听器运行时，模板引用还未被更新。
          因此，使用模板引用的侦听器应该用 flush: 'post' 选项来定义，这将在 DOM 更新后运行回调函数，确保模板引用与 DOM 保持同步，并引用正确的元素。
          */
          flush: 'post'
        }
      )

      return {
        root
      }
    }
  }
</script>