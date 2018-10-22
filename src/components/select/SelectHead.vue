<template>
  <div>
    <div
      v-show="multiple && selectedList.length"
      v-for="(item, index) in selectedList"
      :key="index"
      class="tag">
      <label class="tag__label">{{ item.text }}</label>
      <span
        class="tag__remove"
        @click.stop="hanldeRemove(index)">X</span>
    </div>
    <span
      v-show="selectedText"
      :class="selectedCls">{{ selectedText }}</span>
    <span
      v-show="clearable && selectedList.length"
      :class="[`${prefixCls}__clear`]"
      @click.stop="handleClear"><i>X</i></span>
  </div>
</template>

<script>
const prefixCls = 'my-select'
export default {
  name: 'SelectHead',
  props: {
    selectedList: {
      type: Array,
      default: () => []
    },
    multiple: {
      type: Boolean
    },
    placeholder: {
      type: String
    },
    clearable: {
      type: Boolean
    }
  },
  data () {
    return {
      prefixCls
    }
  },
  computed: {
    selectedText () {
      if (!this.selectedList.length) {
        return this.placeholder
      }
      return this.multiple ? '' : this.selectedList[0].text
    },
    selectedCls () {
      return {
        [`${prefixCls}__selected-value`]: this.selectedList.length,
        [`${prefixCls}__placeholder`]: !this.selectedList.length
      }
    }
  },
  methods: {
    hanldeRemove (index) {
      this.$emit('on-remove', index)
    },
    handleClear () {
      this.$emit('on-clear')
    }
  }
}
</script>
