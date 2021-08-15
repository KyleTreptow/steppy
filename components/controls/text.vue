<template lang="html">
  <div class="control mod--text"
    :class="{
      'state--focused': focused,
      'state--valid': valid,
      'state--flagged': (flagged && !valid)
    }"
  >
    <label :for="inputName">{{ label }}</label>
    <div class="icons">
      <i class="icon icon--alert"></i>
      <i class="icon icon--check"></i>
      <i class="icon icon--edit"></i>
    </div>
    <input v-model="value"
      type="text"
      :id="inputName"
      :name="inputName"
      :placeholder="placeholder"
      :class="{ valid: valid }"
      @focus="focused = true"
      @blur="focused = false"
      autocomplete="off" >
  </div>
</template>

<script>
  import Control from './_control.vue'
  export default {
    extends: Control
  }
</script>
