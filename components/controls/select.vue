<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <select :name="inputName">
      <option value="">- Select Option -</option>
      <option v-for="option in options" :key="option" :value="option">{{ option }}</option>
    </select>
  </div>
</template>

<script>
  export default {
    props: ['label', 'inputName', 'options']
  }
</script>
