<template>
  <div class="panel-u" v-if="!closed">
    <header v-if="title">
      <slot name="title">{{title}}</slot>
      <div class="grow"></div>
      <slot name="header"></slot>
      <button text square @click="toggle" v-if="slidable">
        <i class="fa fa-chevron-down"></i>
      </button>
      <button text square v-if="closable" @click="closed=true">
        <i class="fa fa-close"></i>
      </button>
    </header>
    <transition name="slidedown" v-on:before-leave="setHeight()" v-on:enter="setHeight(height)" v-on:after-enter="unsetHeight">
      <div v-if="show" ref="body">
        <slot></slot>
      </div>
    </transition>
  </div>
</template>
<script>
  export default {
    name: 'panel',
    prefix: 'sa',
    props: {
      title: '',
      slidable: {
        type: Boolean,
        default: false
      },
      closable: {
        type: Boolean,
        default: false
      }
    },
    data: () => ({
      show: true,
      height: null,
      closed: false,
      waiting: false
    }),
    watch: {
      show(val) {
        if (val) return;
        // this.updateHeight()
      }
    },
    mounted() {
      // this.updateHeight()
      window.addEventListener('resize', this.updateHeight)
    },
    destroyed() {
      window.removeEventListener('resize', this.updateHeight)
    },
    methods: {
      updateHeight() {
        if (this.closed) return;
        if (this.$el.classList.contains('h-auto')) {
          this.height = this.$el.offsetHeight;
          return;
        }
        this.$el.classList.add('h-auto');
        this.height = this.$el.offsetHeight;
        this.$el.classList.remove('h-auto');
      },
      setHeight(height) {
        if (height) {
          this.$refs.body.style.height = height;
        } else {
          this.$refs.body.style.height = `${this.$refs.body.offsetHeight}px`;
          this.height = `${this.$refs.body.offsetHeight}px`;
        }
      },
      unsetHeight() {
        this.$refs.body.style.height = `auto`
      },
      async slideDown() {
        this.waiting = true;
        this.show = true;
        await this.$nextTick()
        this.waiting = false;

      },
      async slideUp() {
        this.waiting = true;
        this.show = false;
        await this.$nextTick()
        this.waiting = false;
      },
      async toggle() {
        this.waiting = true;
        this.show = !this.show;
        await this.$nextTick()
        this.waiting = false;
      }
    },
    async updated() {
      if (this.waiting) return;
      await this.$nextTick();
      await this.$nextTick();
      this.updateHeight();
    }
  }
</script>
<style scoped lang="less">
  @import './panel.less';
  .slidedown-enter-active {
    transition: all .3s ease;
  }

  .slidedown-leave-active {
    transition: all .3s ease;
  }

  .slidedown-enter,
  .slidedown-leave-to {
    height: 0!important;
    padding-bottom: 0!important;
    padding-top: 0!important;
  }

  .panel-u {
    overflow: hidden;
    transition: .3s height;
  }

  .panel-u>header {
    display: flex;
    position: relative;
    background: white;
    z-index: 1;
  }

  .panel-u {
    >header {
      margin-bottom: 0;
    }
    >div {
      padding-bottom: 10px;
      padding-top: 10px;
    }
    >div:first-child {
      margin-top: -10px;
    }
    padding-bottom: 0;
  }
</style>