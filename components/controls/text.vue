<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <input type="text" :name="inputName" value="" :placeholder="placeholder" autocomplete="new-password">
  </div>
</template>

<script>
  export default {
    props: ['label', 'inputName', 'placeholder']
  }
</script>
