<template lang="html">
  <div class="control control--text" :state="inputState">
    <label :for="inputName">{{ label }}</label>
    <div class="control__icons">
      <i v-for=" (icon, index) in icons" :type="icon"></i>
    </div>
    <input v-model="value"
      type="text"
      :id="inputName"
      :name="inputName"
      :placeholder="placeholder"
      @focus="focused = true"
      @blur="focused = false"
      autocomplete="off" >
  </div>
</template>

<script>
  import Control from './_control.vue'
  export default {
    extends: Control,
    data () {
      return {
        icons: ['alert', 'check', 'edit']
      }
    },
    computed: {
      inputState () {
        return this.valid ? 'valid' : this.focused ? 'focused' : (this.flagged && !this.valid) ? 'flagged' : ''
      }
    }
  }
</script>
