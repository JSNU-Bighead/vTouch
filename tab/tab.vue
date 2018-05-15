<template>
  <div class="tab">
    <ul class="tab-items">
      <li v-for="(item, index) in tabs" class="tab-item" :class="{active: index === activeIndex}" :key="index" @click="tab(index,item)">
        <slot :tab="item" name="tab">{{ item[textKey] }}</slot>
      </li>
    </ul>
  </div>
</template>
<script>
  export default {
    name:'Tab',
    props:{
      tabs:{
        type:Array,
        default:[]
      },
      textKey:{
        type:String,
        default:'name'
      },
      valueKey:{
        type:[String,Number],
        default:'id'
      }
    },
    data(){
      return {
        activeIndex: 0,
      }
    },
    methods:{
      tab(index,item) {
        this.activeIndex = index;
        this.$emit('change',item);
      },
    }
  }
</script>
<style scoped>
  .tab-items {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    width: 100%;
    background: #fff;
  }

  .tab-item {
    position: relative;
    -webkit-box-flex: 1;
    -ms-flex: 1;
    flex: 1;
    padding: 10px 0;
    font-size: 14px;
    color: #666;
  }

  .tab-item.active {
    color: #1ab394;
  }

  .tab-item.active::after {
    content: " ";
    position: absolute;
    left: 50%;
    bottom: 0;
    -webkit-transform: translateX(-50%);
    transform: translateX(-50%);
    display: block;
    width: 27px;
    height: 2px;
    background: #1ab394;
  }
</style>