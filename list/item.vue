<template>
  <div class="list-item-wrapper" :class="{'border':border}">
    <div class="list-item-left" v-if="left">
      <slot name="left"></slot>
    </div>
    <div class="list-item-content">
      <div class="bx-title">
        <slot name="title">
          {{title}}
        </slot>
        <span class="bx-sub">
          <slot name="subTitle">{{subTitle}}</slot>
        </span>
      </div>
      <div class="bx-describe">
        <slot name="describe">
          {{describe}}
        </slot>
      </div>
    </div>
    <div class="list-item-right" v-if="right">
      <slot name="right"></slot>
    </div>
  </div>
</template>
<script>
  export default {
    props: {
      left: {
        type: Boolean,
        default: false
      },
      title: {
        type: String,
        default: ''
      },
      subTitle: {
        type: String,
        default: ''
      },
      describe: {
        type: String,
        default: ''
      },
      right: {
        type: Boolean,
        default: false
      },
      border: {
        type: Boolean,
        default: false
      }
    },
  }
</script>
<style lang="less">
  .list-item-wrapper {
    box-sizing: border-box;
    padding: 6px;
    display: flex;
    position: relative;
    background: #fff;

    .list-item-content {
      padding: 0 5px;
      width: 100%;
      text-align: left;
      .bx-title {
        display: block;
        font-size: 16px;
        max-width: 100%;
        line-height: 1.75;
        .bx-sub {
          font-size: 13px;
          color: #999;
        }
      }
      .bx-describe {
        font-size: 14px;
        color: #999;
      }
    }
    .list-item-left,
    .list-item-right {
      display: flex;
      width: 40px;
      min-height: 100%;
      align-items: center;
      justify-content: center;
    }
  }

  .list-item-wrapper.border:after {
    content: '';
    position: absolute;
    background-color: #e4e4e4;
    display: block;
    bottom: 0;
    left: 0;
    height: 1px;
    width: 100%;
    -webkit-transform-origin: 50% 100%;
    transform-origin: 50% 100%;
  }
</style>