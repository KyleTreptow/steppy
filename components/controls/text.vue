<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <input v-model="value" type="text" :name="inputName" :placeholder="placeholder" autocomplete="new-password">
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
