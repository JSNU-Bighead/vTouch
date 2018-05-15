<template>
  <div class="page">
    <div class="page-header" v-if="header">
      <slot name="header"></slot>
    </div>
    <div class="page-content" :style="{paddingTop: pt+'px', paddingBottom: pb+'px'}">
      <slot></slot>
    </div>
    <div class="page-footer" v-if="footer">
      <slot name="footer"></slot>
    </div>
  </div>
</template>
<script>
  export default {
    props: {
      header: {
        type: Boolean,
        default: false,
      },
      pt: {
        type: Number,
        default: 0
      },
      footer: {
        type: Boolean,
        default: false,
      },
      pb: {
        type: Number,
        default: 0
      }
    }
  }
</script>
<style scoped lang="less">
  .page{
    width: 100%;
    height: 100%;
    .page-header{
      position: fixed;
      z-index: 999999;
      top:0;
      left: 0;
      width: 100%;
      padding-bottom: 10px;
      background: #f5f5f5;
    }
    .page-footer{
      position: fixed;
      z-index: 5;
      bottom:0;
      left: 0;
      width: 100%;
    }
  }
</style>