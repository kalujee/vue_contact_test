<template>
  <div class="nav-header">
  <div class="col-lg-12 col-sm-12">
    <div class="input-group">
      <input v-model="search" v-on:input="searchContacts" class="form-control search" placeholder="Search...">
      <span class="input-group-btn">
        <!-- <button class="btn btn-default" type="button">Go!</button> -->
        <router-link :to="{name: 'add'}">
          <img src="../../static/plus.png" class="add">
        </router-link>
      </span>
    </div>
  </div>
</div>
</template>

<script>

export default {
  name: 'header',
  data () {
    return {
      search: ''
    }
  },
  methods: {
    searchContacts () {
      this.$emit('search', this.search)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.search {
  margin: 8px 60px 8px 2px;
}
.add {
  width: 40px;
  float: right;
  margin-right: -10px;
}
.nav-header {
  width: 100%;
  height: 50px;
  background: #468f88;
}

</style>
