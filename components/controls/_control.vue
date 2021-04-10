<script>
  export default {
    props: ['label', 'inputName', 'placeholder', 'options'],
    data (){
      return {
        value: ''
      }
    },
    computed: {
      valid: function(){
        return this.value.length ? true : false
      }
    }
  }
</script>
