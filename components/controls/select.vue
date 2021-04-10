<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <select v-model="value" :name="inputName">
      <option value="">- Select Option -</option>
      <option v-for="option in options" :key="option" :value="option">{{ option }}</option>
    </select>
    <div class="flag" :class="{valid: valid}">
      {{ valid ? ('Valid: ' + value) : 'Invalid'}}
    </div>
  </div>
</template>

<script>
  import Control from './_control.vue'
  export default {
    extends: Control
  }
</script>
