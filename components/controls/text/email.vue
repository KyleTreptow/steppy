<script>
  import Text from '../text.vue'
  export default {
    extends: Text,
    computed: {
      valid () {
        return (/(.+)@(.+){2,}\.(.+){2,}/.test(this.value)) ? true : false
      }
    }
  }
</script>
