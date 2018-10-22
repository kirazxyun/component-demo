<template>
  <div id="app">
    <div class="logo">
      <img src="./assets/logo.png">
    </div>
    <div class="row">
      <label class="row__label">
        单选
      </label>
      <div class="row__content">
        <Select
          v-model="selected1"
          :data="localOptions"
          clearable
          filterable></Select>
      </div>
    </div>
    <div class="row">
      <label class="row__label">
        多选
      </label>
      <div class="row__content">
        <Select
          v-model="selected2"
          :multiple="true"
          :data="localOptions"
          clearable>
          <span
            slot="option"
            slot-scope="{ option }">
            {{ option.value }} + {{ option.text }}
          </span>
        </Select>
      </div>
    </div>
    <div class="row">
      <label class="row__label">
        禁用
      </label>
      <div class="row__content">
        <Select
          v-model="selected3"
          :data="localOptions"
          disabled></Select>
      </div>
    </div>
    <div class="row" style="margin-top: 220px;">
      <label class="row__label">
        这是ui结构示例
      </label>
      <div class="row__content">
        <SelectUiDemo></SelectUiDemo>
      </div>
    </div>
  </div>
</template>

<script>
import Select from './components/select'
import SelectUiDemo from './components/select/ui-demo'
import { localOptions, remoteOptions } from './data'
export default {
  name: 'App',
  components: {
    Select,
    SelectUiDemo
  },
  data () {
    return {
      selected1: '',
      selected2: [],
      selected3: 0,
      localOptions,
      remoteOptions: []
    }
  },
  methods: {
    getRemoteOptions () {
      this.remoteOptions = remoteOptions
    }
  }
}
</script>

<style lang="less" scoped>
@label-width: 200px;
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.logo {
  text-align: center;
}
.row {
  margin-bottom: 24px;
  vertical-align: top;
  zoom: 1;

  &__label, &__content {
    font-size: 14px;
  }
  &__label {
    width: @label-width;
    text-align: right;
    vertical-align: middle;
    float: left;
    color: #515a6e;
    line-height: 1;
    padding: 10px 12px 10px 0;
    box-sizing: border-box;
  }
  &__content {
    margin-left: @label-width;
    position: relative;
    line-height: 32px;
  }
}
</style>
