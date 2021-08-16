<script>
  import Text from './text.vue'
  export default {
    extends: Text,
    computed: {
      valid () {
        return (this.value.length >= 4) ? true : false
      }
    }
  }
</script>
