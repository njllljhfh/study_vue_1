<script setup>
  // This starter template is using Vue 3 <script setup> SFCs
  // Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
  import HelloWorld from './components/HelloWorld.vue'

  // dragon
  import comp1 from './components/dragon1/comp1.vue'
  import MyMap from './components/setupProvideInject/MyMap.vue'
  import TemplateRef1 from './components/templateRef/TemplateRef1.vue'
  import TemplateRef2 from './components/templateRef/TemplateRef2.vue'
  import TemplateRef3 from './components/templateRef/TemplateRef3.vue'
  // dragon-end
</script>

<template>
  <img alt="Vue logo" src="./assets/logo.png"/>
  <HelloWorld msg="Hello Vue 3 + Vite"/>

  <!--dragon-->
  <hr>
  <!--测试：响应式变量 -->
  <h2>测试：响应式变量</h2>
  <comp1></comp1>
  <hr>

  <!--测试：setup中的Provide / Inject-->
  <h2>测试：setup中的Provide / Inject</h2>
  <MyMap></MyMap>
  <hr>

  <!--测试：模板引用-->
  <h2>测试：模板引用1</h2>
  <TemplateRef1>
    <template v-slot:name1>
      <p>哈哈</p>
    </template>
  </TemplateRef1>
  <hr>

  <h2>测试：模板引用2 v-for 中的用法</h2>
  <TemplateRef2></TemplateRef2>
  <hr>

  <h2>测试：模板引用3 侦听模板引用</h2>
  <TemplateRef3></TemplateRef3>
  <hr>
  <!--dragon-end-->
</template>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
