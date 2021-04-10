<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <label v-for="option in options" :for="inputName+'_'+option" :key="option" class="option">
      <input type="radio" :name="inputName" :value="option" :id="inputName+'_'+option" />
      <span>{{ option }}</span>
    </label>
  </div>
</template>

<script>
  export default {
    props: ['label', 'inputName', 'options']
  }
</script>
