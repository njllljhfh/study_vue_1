<template>
  <a href="https://v3.cn.vuejs.org/guide/composition-api-introduction.html">组合式API-介绍</a>
</template>

<script>
  import { toRefs } from 'vue'
  import useUserRepositories from '@/composables/userRepository/useUserRepositories'
  import useRepositoryNameSearch from '@/composables/userRepository/useRepositoryNameSearch'
  // useRepositoryFilters.js 的细节没有实现，我们不需要深入了解实现细节，因为这并不是本指南的重点。
  import useRepositoryFilters from '@/composables/userRepository/useRepositoryFilters'

  export default {
    components: { RepositoriesFilters, RepositoriesSortBy, RepositoriesList },
    props: {
      user: {
        type: String,
        required: true
      }
    },
    setup(props) {
      /*
        将我们的响应式对象转换为一组 ref。这些 ref 将保留与源对象的响应式关联
        https://v3.cn.vuejs.org/guide/reactivity-fundamentals.html#%E5%93%8D%E5%BA%94%E5%BC%8F%E7%8A%B6%E6%80%81%E8%A7%A3%E6%9E%84
      */
      const { user } = toRefs(props)

      // 【1.获取用户仓库的功能】
      const { repositories, getUserRepositories } = useUserRepositories(user)

      // 【2.搜索功能】
      const {
        searchQuery,
        repositoriesMatchingSearchQuery
      } = useRepositoryNameSearch(repositories)

      // 【3.过滤功能】
      const {
        filters,
        updateFilters,
        filteredRepositories
      } = useRepositoryFilters(repositoriesMatchingSearchQuery)

      // - - -
      return {
        // 因为我们并不关心未经过滤的仓库
        // 我们可以在 `repositories` 名称下暴露过滤后的结果
        repositories: repositoriesMatchingSearchQuery,
        getUserRepositories,
        searchQuery,
        filters,
        updateFilters
      } // 这里返回的任何内容都可以用于组件的其余部分
    }
  }
  /*
    请记住，我们只触及了组合式 API 的表面以及它允许我们做什么。要了解更多信息，请参阅深入指南。
  */
</script>

<style scoped>

</style>