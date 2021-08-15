<template lang="html">
  <div class="control mod--text" :class="{'state--focused': focused, 'state--valid': valid, 'state--flagged': (flagged && !valid)}">
    <label :for="inputName">{{ label }}</label>
    <input v-model="value"
      type="text"
      :name="inputName"
      :placeholder="placeholder"
      :class="{ valid: valid }"
      @focus="focused = true"
      @blur="focused = false"
      autocomplete="off"
      >
  </div>
</template>

<script>
  import Control from './_control.vue'
  export default {
    extends: Control
  }
</script>
