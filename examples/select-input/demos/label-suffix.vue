<template>
  <div>
    <!-- :popup-props="{ trigger: 'hover' }" -->
    <!-- 前置内容使用 label 自定义，支持同名插槽 label -->
    <t-select-input
      :value="selectValue"
      :popup-visible="popupVisible"
      label="前置内容："
      style="width: 300px"
      placeholder="Please Select"
      clearable
      @popup-visible-change="onPopupVisibleChange"
      @clear="onClear"
    >
      <template #panel>
        <ul class="tdesign-demo__select-input-ul-label-suffix">
          <li v-for="item in options" :key="item.value" @click="() => onOptionClick(item)">
            {{ item.label }}
          </li>
        </ul>
      </template>
      <!-- 后置图标 -->
      <template #suffixIcon>
        <chevron-down-icon />
      </template>
    </t-select-input>
    <br /><br />

    <!-- 后置内容使用 suffix 自定义，支持同名插槽 suffix -->
    <t-select-input
      :value="selectValue"
      :popup-visible="popupVisible2"
      suffix="单位：元"
      style="width: 300px"
      placeholder="Please Select"
      clearable
      @popup-visible-change="onPopupVisibleChange2"
      @clear="onClear"
    >
      <template #panel>
        <ul class="tdesign-demo__select-input-ul-label-suffix">
          <li v-for="item in options" :key="item.value" @click="() => onOptionClick(item)">
            {{ item.label }}
          </li>
        </ul>
      </template>
      <template #suffixIcon>
        <chevron-down-icon />
      </template>
    </t-select-input>
  </div>
</template>
<script>
import { ChevronDownIcon } from 'tdesign-icons-vue';

const options = [
  // 全选
  { label: 'Check All', checkAll: true },
  { label: 'tdesign-vue', value: 1 },
  { label: 'tdesign-react', value: 2 },
  { label: 'tdesign-miniprogram', value: 3 },
  { label: 'tdesign-angular', value: 4 },
  { label: 'tdesign-mobile-vue', value: 5 },
  { label: 'tdesign-mobile-react', value: 6 },
];

export default {
  components: {
    ChevronDownIcon,
  },
  data() {
    return {
      options,
      selectValue: { label: 'tdesign-vue', value: 1 },
      popupVisible: false,
      popupVisible2: false,
    };
  },
  methods: {
    onOptionClick(item) {
      this.selectValue = item;
      // 选中后立即关闭浮层
      this.popupVisible = false;
      this.popupVisible2 = false;
    },
    onClear() {
      this.selectValue = undefined;
    },
    onPopupVisibleChange(val, context) {
      console.log(context);
      this.popupVisible = val;
    },
    onPopupVisibleChange2(val) {
      this.popupVisible2 = val;
    },
  },
};
</script>
<style lang="less" scoped>
.tdesign-demo__select-input-ul-label-suffix {
  padding: 4px 0;
}
.tdesign-demo__select-input-ul-label-suffix > li {
  display: block;
  border-radius: 3px;
  height: 40px;
  line-height: 22px;
  cursor: pointer;
  padding: 9px 8px;
  color: var(--td-text-color-primary);
  transition: background-color 0.2s cubic-bezier(0.38, 0, 0.24, 1);
  white-space: nowrap;
  word-wrap: normal;
  overflow: hidden;
  text-overflow: ellipsis;
}

.tdesign-demo__select-input-ul-label-suffix > li:hover {
  background-color: var(--td-bg-color-container-hover);
}
</style>
