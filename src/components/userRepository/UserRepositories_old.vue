<template>
  <a href="https://v3.cn.vuejs.org/guide/composition-api-introduction.html">组合式API-介绍</a>
</template>

<script>
  /*
  WARNING
  在 setup 中你应该避免使用 this，因为它不会找到组件实例。
  setup 的调用发生在 data property、computed property 或 methods 被解析之前，所以它们无法在 setup 中被获取。
  */
  import {fetchUserRepositories} from '@/api/repositories'
  import {ref, onMounted, watch, toRefs, computed} from 'vue'

  export default {
    components: {RepositoriesFilters, RepositoriesSortBy, RepositoriesList},
    props: {
      user: {
        type: String,
        required: true
      }
    },
    setup(props) {
      // 【1.获取用户仓库的功能】
      // 使用 `toRefs` 创建对 `props` 中的 `user` property 的响应式引用
      const {user} = toRefs(props)

      const repositories = ref([])
      const getUserRepositories = async () => {
        // 更新 `prop.user` 到 `user.value` 访问引用值
        repositories.value = await fetchUserRepositories(user.value)
      }

      //组合式 API 上的生命周期钩子与选项式 API 的名称相同，但前缀为 on：即 mounted 看起来会像 onMounted。
      //这些函数接受一个回调，当钩子被组件调用时，该回调将被执行。
      onMounted(getUserRepositories) // 在 `mounted` 时调用 `getUserRepositories`

      // 在 user prop 的响应式引用上设置一个侦听器
      watch(user, getUserRepositories)
      // - - -

      // 【2.搜索功能】
      const searchQuery = ref('')
      const repositoriesMatchingSearchQuery = computed(() => {
        // 过滤后的 repositories
        return repositories.value.filter(
          repository => repository.name.includes(searchQuery.value)
        )
      })
      // - - -

      // 【3.过滤功能】
      // pass
      // - - -

      return {
        repositories,
        getUserRepositories, // 返回的函数与方法的行为相同
        searchQuery,
        repositoriesMatchingSearchQuery
      } // 这里返回的任何内容都可以用于组件的其余部分
    },
    data() {
      return {
        filters: {...}, // 3
        // searchQuery: '' // 2
      }
    },
    computed: {
      filteredRepositories() { ... }, // 3
      // repositoriesMatchingSearchQuery () { ... }, // 2
    },
    // watch: {
    //   user: 'getUserRepositories' // 1
    // },
    methods: {
      updateFilters() { ... }, // 3
    },
    // mounted () {
    //   this.getUserRepositories() // 1
    // }
  }
</script>

<style scoped>

</style>