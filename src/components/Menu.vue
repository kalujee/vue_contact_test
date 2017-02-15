<template>
    <button v-on:click="remove" class="btn btn-danger">DELETE</button>
</template>

<script>

export default {
  name: 'menu',
  props: ['show'],
  data () {
    return {
    }
  },
  methods: {
    setStyle (px) {
      this.styleA = {'margin-right': px}
    },
    remove () {
      var self = this;
      $.confirm({
            columnClass: 'col-md-4 col-md-offset-4',
            animation: 'zoom',
            closeAnimation: 'scale',
            title:"Delete",
            content:"Confirm to delete the contact?",
            buttons: {
                confirm:{
                    text: 'Confirm',
                    action: function(){
                      self.$emit('remove')
                    }
                },
                cancel: {
                    text: "Cancel"
                }
            }
        });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.menu {
  margin-right: 0px;
}

</style>
