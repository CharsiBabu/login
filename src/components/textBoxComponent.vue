<template>
  <div class="input-wrapper">
    <i class="icon fa" v-if="showIcon" :class="iconClass"></i>
    <input :type="type" name="" @input="handleInput" :placeholder="placeholder" id=""/>
  </div>
</template>

<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: 'Enter data'
    },
    type: {
      type: String,
      default: 'text'
    },
    showIcon: {
      default: false,
      type: Boolean
    },
    iconClass: {
      type: String,
      default: 'icon'
    }
  },
  methods: {
    handleInput (ev) {
      this.$emit('input', ev.target.value)
    }
  }
}
</script>
<style scoped>
input{
  padding: 10px;
  padding-left: 45px;
  width: 200px;
  border:1px solid;
  border-radius: 5px;
  border-color: rgba(0, 0, 0, 0.2);
}
.input-wrapper{
  position:relative;
}
.icon{
  position: absolute;
  left: 20px;
  top: 11px;
  color: orange;
}
</style>
