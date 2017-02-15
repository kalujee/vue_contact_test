<template>
  <div>
    <top-header v-on:search="search"></top-header>
    <div v-for="item in contacts">
      <contact-item :value="item">
      </contact-item>
    </div>
  </div>
</template>

<script>

import Header from './Header.vue'
import ContactItem from './ContactItem.vue'

export default {
  name: 'index',
  data () {
    return {
      total_data: [],
      contacts: []
    }
  },
  methods: {
    getData () {
      // console.log($)
      var self = this;
      $.ajax({
        type: 'get',
        async: false,
        url: 'http://localhost:8089/contacts',
        dataType: 'json',
        success: function (data) {

          self.contacts = data
          self.total_data = self.contacts
        },
        error: function () {
          alert('fail')
        }
      })
    },
    search (data) {
      var tmp = []
      for (var i = 0; i < this.total_data.length; ++i) {
        var d = this.total_data[i]
        if (d.first_name.indexOf(data) >= 0 || d.last_name.indexOf(data) >= 0 ||
          d.email.indexOf(data) >= 0) {
          tmp.push(d)
        }
      }
      this.contacts = tmp
    }
  },
  components: {
    'top-header': Header,
    'contact-item': ContactItem
  },
  mounted: function () {
    this.getData()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
