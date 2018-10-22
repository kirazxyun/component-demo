<template>
  <div>
    <div class="my-select my-select--single">
      <div class="my-select__selection">
        <div>
          <input
            type="text"
            class="my-select__input"
            placeholder="请选择"
            autocomplete="off"/>
          <!-- <span class="my-select__selected-value">选中值</span> 不过滤的时候选中值展示结构 -->
          <!-- <span class="my-select__placeholder">placeholder</span> 不过滤的时候placeholder展示结构 -->
          <span class="my-select__clear"><i>X</i></span>
        </div>
      </div>

      <div class="my-select__dropdown">
        <ul class="my-select__not-found">
          <li>暂无数据</li>
        </ul>
        <ul class="my-select__dropdown-list">
          <li class="my-select__item">选项</li>
          <li class="my-select__item my-select__item--disabled">禁用</li>
          <li class="my-select__item my-select__item--selected">选中</li>
          <li class="my-select__item my-select__item--focus">focus</li>
        </ul>
        <ul class="my-select__loading">
          加载中
        </ul>
      </div>
    </div>

    <div class="my-select my-select--multiple" style="margin-top: 220px;">
      <div class="my-select__selection">
        <div>
          <div class="tag">
            <label class="tag__label">label</label>
            <span class="tag__remove">X</span>
          </div>
          <span class="my-select__clear"><i>X</i></span>
        </div>
      </div>
      <div class="my-select__dropdown">
        <ul class="my-select__not-found">
          <li>暂无数据</li>
        </ul>
        <ul class="my-select__dropdown-list">
          <li class="my-select__item">选项</li>
          <li class="my-select__item my-select__item--disabled">禁用</li>
          <li class="my-select__item my-select__item--selected">选中</li>
          <li class="my-select__item my-select__item--focus">focus</li>
        </ul>
        <ul class="my-select__loading">
          加载中
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped lang="less">
@import 'style.less';
</style>
