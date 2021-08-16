<script>
  import Text from '../text.vue'
  export default {
    extends: Text,
    data () {
      return {
        tooltip: 'Must be a valid email address'
      }
    },
    computed: {
      valid () {
        return (/(.+)@(.+){2,}\.(.+){2,}/.test(this.value)) ? true : false
      }
    }
  }
</script>
