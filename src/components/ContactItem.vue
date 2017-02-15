<template>
  <div class="user" v-on:click="clicked" v-on:touchstart="mousedown" v-on:touchmove="move" v-on:touchend="up">
      <img class="avatar"  v-on:click="clicked" src="../../static/user.png" alt="">
      <div class="user-name">
          <a href="#">{{value.first_name}} · {{value.last_name}}</a>
      </div>
      <div class="email">
        <span class="contact-type"><i class="fa fa-envelope"> </i>
          </span>
          <span>{{value.email}}</span>
      </div>
      <!-- <del-menu class="menu" v-on:remove="remove"></del-menu> -->
  </div>
  
</template>

<script>

export default {
  name: 'item',
  props: {
    value: {
      type: Object,
      default: function () {
        return {
          'first_name': '',
          'last_name': '',
          'email': ''
        }
      }
    }
  },
  mounted () {
    
  },
  data () {
    return {
      down: false,
      editable: false,
      startpos: 0,
      offset: 0
    }
  },
  methods: {
    edit () {
      
    },
    move (event) {
      if (this.down) {
        this.offset = this.startpos - event.touches[0].clientX
      }
    },
    up (event) {
      this.down = false
      if (this.offset > 40) {
        this.$children[0].setStyle('0px')
      }
    },
    mousedown (event) {
      this.down = true
      this.startpos = event.touches[0].clientX;
    },
    clicked (event) {
      this.$router.push({path:'/edit/' + this.value.id})
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search {
}
.add {
  width: 40px;
  float: right;
}
.users {
    overflow-y: auto;
}
.avatar {
    white: 36px;
    height: 36px;
    float: left;
    margin-right: 10px;
}
.user {
  padding: 8px 10px;
  border-bottom: 1px solid #e7eaec;
}
.user-name {
    padding: 10px;
    padding-top: 0px;
}
.email {
  margin-left: 45px;
  margin-top: -10px;
  color: #9D9D9D
}
.menu {
  display: inline-block;
  float: right;
  margin-top: -40px;
  z-index: 999;
}

</style>
