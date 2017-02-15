<template>
  <div class="layer-wrap" v-if="deleteStatus">
    <div class="layer-content">
      <h3 class="layer-title">清单名称</h3>
      <div class="txt-content">您确认要删除该清单？</div>
      <div class="button-wrap clearfix">
        <button class="cancel" v-touch:tap="cancel">取消</button>
        <button class="confirm" v-touch:tap="confirm">确认</button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" src="./message.scss" scoped></style>

<script>
  var methods = {
  cancel: function() {
    // this.$dispatch('delete_cancel');
  },
  confirm: function() {
    // this.$dispatch('delete_confirm');
  }
};

export default {
  data: function() {
    return {}
  },
  props: ['deleteStatus'],
  methods: methods,
  ready: function() {
  }
}
</script>
