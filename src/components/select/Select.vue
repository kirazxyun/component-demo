<template>
  <div
    :class="classes">
    <div
      :class="selectionCls"
      @click="handleDropToggle">
      <slot>
        <SelectHead
          :selected-list="selectedList"
          :placeholder="placeholder"
          :clearable="clearable"
          :multiple="multiple"
          @on-remove="handleRemove"
          @on-clear="handleClear"></SelectHead>
      </slot>
    </div>
    <SelectDrop
      :class="dropdownCls"
      v-show="isDropOpen">
      <input
        v-if="filterable"
        v-model="key"
        type="text"
        :class="[`${prefixCls}__input`]"
        :placeholder="searchPlaceholder"
        autocomplete="off"/>
      <ul
        v-show="!resultData.length"
        :class="[`${prefixCls}__not-found`]">
        <li>{{ noFoundText }}</li>
      </ul>
      <ul
        v-show="resultData.length"
        :class="[`${prefixCls}__dropdown-list`]">
        <li
          v-for="(item, index) in resultData"
          :key="index"
          :class="getItemCls(item)"
          @click="handleSelected(item)">
          <slot
            name="option"
            :option="item">{{ item.text }}</slot>
        </li>
      </ul>
    </SelectDrop>
  </div>
</template>

<script>
import SelectHead from './SelectHead'
import SelectDrop from './SelectDrop'

const prefixCls = 'my-select'

export default {
  name: 'MySelect',
  components: {
    SelectHead,
    SelectDrop
  },
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
    filterable: {
      type: Boolean,
      default: false
    },
    disabled: {
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
      prefixCls,
      isDropOpen: false,
      key: '' // 搜索关键字
    }
  },
  computed: {
    classes () {
      return [
        prefixCls,
        {
          [`${prefixCls}--single`]: !this.multiple,
          [`${prefixCls}--multiple`]: this.multiple,
          [`${prefixCls}--disabled`]: this.disabled
        }
      ]
    },
    selectionCls () {
      return [
        `${prefixCls}__selection`
      ]
    },
    dropdownCls () {
      return [
        `${prefixCls}__dropdown`
      ]
    },
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
    resultData () {
      if (!this.key) return this.data

      const key = this.key.toLowerCase()
      return this.data.filter(item => item.text.toLowerCase().indexOf(key) > -1)
    }
  },
  mounted () {
    this.attachEvents()
  },
  destroyed () {
    this.removeEvents()
  },
  watch: {
  },
  methods: {
    attachEvents () {
      document.addEventListener('click', this.handleDocumentClick)
    },
    removeEvents () {
      document.removeEventListener('click', this.handleDocumentClick)
    },
    handleDocumentClick (e) {
      if (this.$el.contains(e.target)) {
        return false
      }
      this.handleDropClose()
    },
    getItemCls (item) {
      return [
        `${prefixCls}__item`,
        {
          [`${prefixCls}__item--selected`]: this.currentVal.indexOf(item.value) > -1
        }
      ]
    },
    handleDropOpen () {
      this.isDropOpen = true
    },
    handleDropClose () {
      this.isDropOpen = false
    },
    handleDropToggle () {
      if (this.disabled) return
      this.isDropOpen = !this.isDropOpen
    },
    handleRemove (index) {
      let result = [...this.currentVal]
      result.splice(index, 1)
      this.afterChange(result)
    },
    handleClear () {
      this.afterChange([])
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
      this.afterChange(result)
    },
    afterChange (result) {
      this.$emit('input', result)
      this.$emit('change', result)
      this.$emit('on-change', result)
    }
  }
}
</script>

<style lang="less">
@import './style.less';
</style>
