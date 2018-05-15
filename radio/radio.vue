<template>
  <label @click.stop="handleClick" class="bx-radio">
    <input type="radio" :disabled="disabled" :value="nativeValue" @change="handleChange" v-model="inputValue">
    <i class="icon-radio" :class="{disabled:disabled}"></i>
  </label>
</template>

<script>
export default {
  name: 'bx-radio',
  props: {
    value: {},
    nativeValue: {
      default:null
    },
    disabled: {
      type: Boolean,
      default: false
    },
  },
  data () {
    return {
      inputValue: this.value
    }
  },
  watch: {
    value (val) {
      this.inputValue = val
    },
    inputValue (val) {
      this.$emit('input', val)
    }
  },
  methods: {
    handleClick () {
      // 阻止事件冒泡，放置外部控制的时候触发两次 click
    },
    handleChange () {
      this.$emit('change', this.inputValue)
    }
  },
}
</script>

<style lang="less">
.bx-radio {
  position: relative;
  display: inline-block;
  input[type="radio"] {
    display: none;
  }
  * {
    pointer-events: none;
  }
  .icon-radio{
    display: block;
    width: 18px;
    height: 18px;
    border-radius: 9px;
    background-image: url('https://file.40017.cn/publicfront/bxTouch/radio-no.svg');
    background-repeat: no-repeat; 
    background-size: 18px 18px;
  }
  .icon-radio.disabled  {
    cursor: not-allowed;
    background-image: url('https://file.40017.cn/publicfront/bxTouch/radio-disabled.svg');
    background-repeat: no-repeat; 
    background-size: 18px 18px;
  }
  input:checked~.icon-radio{
    background-image: url('https://file.40017.cn/publicfront/bxTouch/radio-yes.svg');
    background-repeat: no-repeat; 
    background-size: 18px 18px;
  }
}
</style>
