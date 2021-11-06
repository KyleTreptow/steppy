<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <div class="options">
      <label v-for="option in options" :for="inputName+'_'+option" :key="option" class="option">
        <input v-model="value" type="checkbox" :name="inputName" :value="option" :id="inputName+'_'+option" />
        <span>{{ option }}</span>
      </label>
    </div>
    <!--
    <div class="flag" :class="{valid: valid}">
      {{ valid ? ('Valid: ' + value) : 'Invalid'}}
    </div> 
    -->
  </div>
</template>

<script>
  import Control from './_control.vue'
  export default {
    extends: Control,
    data () {
      return {
        value: []
      }
    }
  }
</script>
