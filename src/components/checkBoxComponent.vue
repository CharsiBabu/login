<template>
<label for="chkbox" class="checkbox">
  <input type="checkbox" @change="handleInput" name="chkbox" id="chkbox"/>
  <span>{{label}}</span>
</label>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: 'Remember me'
    }
  },
  methods: {
    handleInput (ev) {
      this.$emit('change', ev.target.checked)
    }
  }
}
</script>
