<template>
  <div class="dialog-attach-wrap">
    <!-- attach挂载 -->
    <t-button theme="primary" @click="visibleBody = true">挂载在body</t-button>
    <t-button theme="primary" @click="visibleIdAttach = true">挂载特定元素</t-button>
    <t-button theme="primary" @click="visibleFunctionAttach = true">挂载函数返回节点</t-button>
    <t-button theme="primary" @click="visibleShowInAttachedElement = true">展示在挂载元素区域</t-button>

    <t-dialog
      :visible.sync="visibleBody"
      attach="body"
      header="挂载在body"
      destroyOnClose
      :onConfirm="() => (this.visibleBody = false)"
    >
      <div slot="body">
        <div>被挂载到 body 元素的对话框</div>
      </div>
    </t-dialog>

    <t-dialog
      :visible.sync="visibleIdAttach"
      attach="#app"
      header="挂载到id为app的元素"
      destroyOnClose
      :onConfirm="() => (this.visibleIdAttach = false)"
    >
      <div slot="body">
        <div>通过querySelect指定元素挂载</div>
        <div>支持原生document.querySelect选择元素</div>
        <div>querySelect获取到的第一个元素为挂载点</div>
      </div>
    </t-dialog>

    <t-dialog
      :visible.sync="visibleFunctionAttach"
      :attach="getAttach"
      header="函数返回挂载节点"
      destroyOnClose
      :onConfirm="() => (this.visibleFunctionAttach = false)"
    >
      <div slot="body">
        <div>指定函数返回的节点为挂载点</div>
        <div>函数返回为DOM节点对象</div>
      </div>
    </t-dialog>

    <t-dialog
      :visible.sync="visibleShowInAttachedElement"
      header="对话框仅展示在挂载元素区域"
      :showInAttachedElement="true"
      placement="center"
      :onConfirm="() => (this.visibleShowInAttachedElement = false)"
    >
      <div slot="body">
        <div>父元素（挂载元素）需要有定位属性，如：position: relative</div>
        <div>showInAttachedElement API 仅针对模态对话框有效</div>
      </div>
    </t-dialog>
  </div>
</template>
<script>
import Vue from 'vue';

export default Vue.extend({
  data() {
    return {
      visibleBody: false,
      visibleIdAttach: false,
      visibleFunctionAttach: false,
      visibleShowInAttachedElement: false,
    };
  },
  methods: {
    getAttach() {
      return this.$root.$el;
    },
  },
});
</script>
<style>
.t-button {
  margin-right: 20px;
}
.dialog-attach-wrap {
  position: relative;
  height: 400px;
  padding: 20px;
  border: 1px solid #ebedf0;
  border-radius: 2px;
  overflow: hidden;
}
body {
  width: 3000px;
}
</style>
