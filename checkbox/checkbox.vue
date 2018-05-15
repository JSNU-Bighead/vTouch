<template>
  <label @click.stop="handleClick" class="bx-checkbox">
    <input type="checkbox" :disabled="disabled" :value="nativeValue" @change="handleChange" v-model="inputValue">
    <i class="icon-checkbox" :class="{disabled:disabled}"></i>
  </label>
</template>

<script>
export default {
  name: 'bx-checkbox',
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
.bx-checkbox {
  position: relative;
  display: inline-block;
  input[type="checkbox"] {
    display: none;
  }
  * {
    pointer-events: none;
  }
  .disabled  {
    cursor: not-allowed;
    background-color: #ccc;
    border-radius: 2px;
  }
  .icon-checkbox{
    display: block;
    width: 18px;
    height: 18px;
    background-image: url('https://file.40017.cn/publicfront/bxTouch/checkbox-no.svg');
    background-repeat: no-repeat; 
    background-size: 18px 18px;
  }
  input:checked~.icon-checkbox{
    background-image: url('https://file.40017.cn/publicfront/bxTouch/checkbox-yes.svg');
    background-repeat: no-repeat; 
    background-size: 18px 18px;
  }
}
</style>
