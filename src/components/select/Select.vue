<template>
  <div class="my-select">
    <div
      class="my-select__header"
      @click="handleDropToggle">
      <slot>
        {{ displayText }}
      </slot>
    </div>
    <div
      class="my-select__drop"
      v-if="isDropOpen">
      <input
        type="text"
        class="search-input"
        :placeholder="searchPlaceholder"
        v-model="key"
        autocomplete="off"/>
      <div class="content">
        <ul
          v-show="resultData.length"
          class="list">
          <li
            v-for="(item, index) in resultData "
            :key="index"
            class="list__item"
            :class="{active: isItemSelected(item)}"
            @click="handleSelected(item)">
              {{item.text}}
          </li>
        </ul>
        <p
          v-show="!resultData.length"
          class="noFound">
          {{ noFoundText }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MySelect',
  props: {
    value: {
      type: [String, Array, Number],
      default: ''
    },
    data: {
      type: Array,
      default: () => []
    },
    multiple: {
      type: Boolean,
      default: false
    },
    clearable: {
      type: Boolean,
      default: false
    },
    placeholder: {
      type: String,
      default: '请选择'
    },
    searchPlaceholder: {
      type: String,
      default: '请输入关键字'
    },
    noFoundText: {
      type: String,
      default: '暂无数据'
    }
  },
  data: function () {
    return {
      isDropOpen: false,
      key: '' // 搜索关键字
    }
  },
  computed: {
    currentVal () {
      if (Array.isArray(this.value)) {
        return [...this.value]
      } else {
        return [this.value]
      }
    },
    selectedList () {
      return this.data.filter(item => this.currentVal.indexOf(item.value) > -1)
    },
    displayText () {
      if (!this.selectedList.length) return this.placeholder
      return this.selectedList.map(item => item.text).join(',')
    },
    resultData () {
      if (!this.key) return this.data

      const key = this.key.toLowerCase()
      return this.data.filter(item => item.text.toLowerCase().indexOf(key) > -1)
    }
  },
  watch: {
  },
  methods: {
    handleDropOpen () {
      this.isDropOpen = true
    },
    handleDropClose () {
      this.isDropOpen = false
    },
    handleDropToggle () {
      this.isDropOpen = !this.isDropOpen
    },
    isItemSelected (item) {
      return this.currentVal.indexOf(item.value) > -1
    },
    handleSelected (item) {
      const index = this.currentVal.indexOf(item.value)
      if (!this.multiple && index > -1) return

      let result = []

      if (this.multiple) {
        result = [...this.currentVal]
      }

      if (index > -1) {
        result.splice(index, 1)
      } else {
        result.push(item.value)
        if (!this.multiple) this.handleDropClose()
      }

      if (!this.multiple) {
        result = result[0]
      }
      this.$emit('input', result)
      this.$emit('change', result)
      this.$emit('on-change', result)
    }
  }
}
</script>

<style scoped lang="scss">
@import './style.scss';
</style>
