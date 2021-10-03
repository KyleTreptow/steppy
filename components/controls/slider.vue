<template lang="html">
  <div class="control">
    <label :for="inputName">{{ label }}</label>
    <h2>{{ value }}</h2>
    <vue-slider v-model="value" :min="0" :max="100" :lazy="false" tooltip="none" :marks="value => value % 20 === 0" />
  </div>
</template>

<script>
  import Control from './_control.vue'
  import VueSlider from 'vue-slider-component'
  import 'vue-slider-component/theme/antd.css'
  export default {
    extends: Control,
    components: { VueSlider },
    data () {
      return{
        value: 50
      }
    },
    computed: {
      valid () {
        return true
      }
    }
  }
</script>
