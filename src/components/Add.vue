<template>
  <div>
    <nav-item title="Add Contact"></nav-item>
    <div class="addform">
      <form @submit.prevent="submit" class="form-horizontal">
        <div class="form-group">
          <label for="name">First Name</label>
          <input type="text" class="form-control" v-model="first_name" placeholder="First Name">
        </div>
        <div class="form-group">
          <label for="name">Last Name</label>
          <input type="text" class="form-control" v-model="last_name" placeholder="Last Name">
        </div>
        <div class="form-group">
          <label for="name">Email</label>
          <input type="text" class="form-control" v-model="email" placeholder="youemail@gmail.com">
        </div>
        <div class="form-group">
          <label for="name">Description</label>
          <input type="text" class="form-control" v-model="description" placeholder="Description">
        </div>
        <div class="center-btn">
          <button type="submit" class="btn btn-success">  Add  </button>
        </div>
        
      </form>
    </div>
  </div>
</template>

<script>
import Navigate from './Navigate.vue'
export default {
  name: 'add',
  data () {
    return {
      first_name: '',
      last_name: '',
      email: '',
      description: ''
    }
  },
  components: {
    'nav-item': Navigate
  },
  computed: {
    validation () {
      return {
        first_name: !!this.first_name.trim(),
        last_name: !!this.last_name.trim(),
        description: !!this.description.trim(),
        email: /^(\w)+(\.\w+)*@(\w)+((\.\w{2,3}){1,3})$/.test(this.email)
      }
    },
    isValid () {
      const validation = this.validation
      console.log(validation)
      return Object.keys(validation).every(key => validation[key])
    }
  },
  methods: {
    submit () {
      if (this.isValid) {
        var data = {first_name: this.first_name, last_name: this.last_name,
                  email: this.email, description: this.description}
        $.ajax({
          type: 'post',
          async: false,
          url: 'http://localhost:8089/contacts',
          data: data,
          dataType: 'json',
          success: function (data) {
            $.toast({
              heading: 'Complete',
              text: 'Add a new contact',
              icon: 'success',
              loader: false,
              position: 'mid-center',
              hideAfter: 1500,
              afterHidden: function () {
                window.history.back()
              }
            })
          },
          error: function (err) {
            console.log(err.responseJSON.message)
            $.toast({
              heading: '请求API失败:' + err.responseJSON.message,
              icon: 'error',
              loader: false
            })
          }
        })
      } else {
        $.toast({
          text: 'Input not complete',
          heading: 'Info',
          icon: 'error',
          loader: false
        })
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.addform {
  margin: 30px;
}
.center-btn {
  text-align: center;
}
</style>
