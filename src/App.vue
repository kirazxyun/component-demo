<template>
  <div id="app">
    <!-- <ThePanel></ThePanel> -->
    <img src="./assets/logo.png">
    单选：
    <Select
      v-model="selected1"
      :data="selectSourceData"></Select>
    多选：
    <Select
      v-model="selected2"
      :multiple="true"
      :data="selectSourceData"></Select>
  </div>
</template>

<script>
import Select from './components/select'
import ThePanel from './demo/Scoped'
export default {
  name: 'App',
  components: {
    Select,
    ThePanel
  },
  data () {
    return {
      selected1: '',
      selected2: [],
      selectSourceData: [
        {
          text: 'wofsdf',
          value: 0
        },
        {
          text: '我是技术渣1',
          value: 1
        },
        {
          text: '我是技术渣2',
          value: 2
        },
        {
          text: '我是天坑',
          value: 3
        },
        {
          text: '我是天坑,分身乏术',
          value: 4
        },
        {
          text: '我是天坑2,分身乏术',
          value: 5
        },
        {
          text: '我是天坑3,分身乏术',
          value: 6
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
