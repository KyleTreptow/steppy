<template lang="html">
  <div class="control control--text" :state="inputState">
    <div class="control__tooltip">
      {{ tooltip }}
    </div>
    <label :for="inputName">{{ label }}</label>
    <div class="control__icons">
      <i v-for=" (icon, index) in icons" :type="icon" :key="icon+'-'+index"></i>
    </div>
    <input v-model="value"
      type="text"
      :id="inputName"
      :name="inputName + '_x'"
      :placeholder="placeholder"
      @focus="focused = true"
      @blur="focused = false"
      autocomplete="no" >
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
