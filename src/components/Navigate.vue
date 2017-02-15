<template>
  <header class="nav-header">
    <div class="back">
      <img src="../../static/back.png" class="icon-left" v-on:click="back">
    </div>
    <div class="text-center">
      <span class="header-txt">{{title}}</span>
    </div>
    <div v-if="showDelete" class="delete">
      <del-menu v-on:remove="remove"></del-menu>
    </div>
  </header>
</template>

<script>
import Menu from './Menu.vue'
export default {
  name: 'navigate',
  props: {
    title: {
      type: String
    },
    showDelete: {
      type: Boolean,
      default: false
    }
  },
  components: {
    'del-menu': Menu
  },
  data () {
    return {
      search: ''
    }
  },
  methods: {
    back () {
      console.log('--back')
      window.history.back()
    },
    remove () {
      this.$emit('remove')
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.delete {
  display: inline-block;
  float: right;
  margin-top: -40px;
  margin-right: 10px;
}
.back {
  float: left;
  display: inline-block;
  height: 50px;
}
.text-center {
  display: inline-block;
  text-align: center;
  /*width: 80%;*/
  width: 70%;
  height: 50px;
  line-height: 50px;
  vertical-align: middle;
}
.nav-header {
  width: 100%;
  height: 50px;
  background: #468f88;
  color: #fff;
  .icon-left {
    display: inline-block;
    float: left;
  }
  .header-txt {
    margin-left: 40px;
    margin-right: 40px;
    
    display: inline-block;
    width: auto;
    height: 50px;
    line-height: 50px;
    font-size: 20px;
    color: #fff;
  }
}

</style>
