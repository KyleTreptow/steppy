<script>
  export default {
    props: ['label', 'inputName', 'placeholder', 'options', 'panel'],
    data () {
      return {
        value: ''
      }
    },
    computed: {
      valid () {
        return this.value.length ? true : false
      }
    },
    watch: {
      value () {
        if(this.valid) {
          // call parent fn to add inputName
          this.$parent.removeErrorFlag(this.inputName, this.panel)
        } else {
          // call parent fn to remove inputName
          this.$parent.addErrorFlag(this.inputName, this.panel)
        }
      }
    },
    mounted () {
      if(this.valid) {
        // call parent fn to add inputName
        this.$parent.removeErrorFlag(this.inputName, this.panel)
      } else {
        // call parent fn to remove inputName
        this.$parent.addErrorFlag(this.inputName, this.panel)
      }
    }
  }
</script>
