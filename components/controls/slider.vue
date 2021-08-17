<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <vue-slider v-model="value" />
  </div>
</template>

<script>
  import Control from './_control.vue'
  import VueSlider from 'vue-slider-component'
  import 'vue-slider-component/theme/antd.css'
  export default {
    extends: Control,
    components: { VueSlider },
    computed: {
      valid () {
        return true
      }
    }
  }
</script>
