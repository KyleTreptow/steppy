<template>
    <div class="wrap">
      <form class="" action="/" method="post" autocomplete="off">
        <header class="header">
          <div class="progress">
            Progress:
            <b>{{ progress }}</b> (Step {{ step + 1 }} of {{ panels.length }})
          </div>
          <div class="bubbles">
            <button v-for="(i, index) in panels" :key="index+'_button'"
            type="button" :class="{ active: step == index }" @click="step = index">{{ index + 1 }}</button>
          </div>
        </header>
        <main>
          <div v-for="(i, index) in panels" :key="index+'_panel'"
          class="panel" :class="{ before: step > index, active: step == index, after: step < index }">
          <header>
            <h1>
              <!-- <span>{{ step + 1 }}</span> -->
              {{ i.title }}
            </h1>
          </header>
          <div class="panel__fields">
            <div v-for="input in i.inputs" :key="input.inputName">
              <component :is="input.type"
                :label="input.label"
                :inputName="input.inputName"
                :placeholder="input.placeholder"
                :options="input.options"
                :panel="index"
              />
            </div>
          </div>
          <footer>
            <button type="button" @click="nextPanel(index)" class="button">Next</button>
            <div class="well">Errors:
              <ul>
                <li v-for="error in errors[index]" :key="error">{{ error }}</li>
              </ul>
            </div>
          </footer>
          </div>
        </main>
      </form>
    </div>
</template>

<script>
    import('./assets/css/main.css');
    import TextControl from './components/controls/text.vue'
    import RadioControl from './components/controls/radio.vue'
    import CheckboxControl from './components/controls/checkbox.vue'
    import SelectControl from './components/controls/select.vue'
    import appData from './appData.json'
    export default {
      components: { TextControl, RadioControl, CheckboxControl, SelectControl },
      data () {
        return {
          panels: appData.panels,
          step: 0,
          errors: appData.panels.map(function(){ return new Array(0) })
        }
      },
      computed: {
        progress () {
          return ((this.step +1 ) / this.panels.length) * 100 + '%'
        }
      },
      methods: {
        addErrorFlag (flag, panel) {
          let e = this.errors
          if(!e[panel].includes(flag)){
            e[panel].push(flag)
          }
          this.errors = []
          this.errors = e
        },
        removeErrorFlag (flag, panel) {
          console.log(this.errors)
          let filtered = this.errors[panel].filter(function(value){
            return value != flag;
          })
          let e = this.errors
          this.errors = []
          e[panel] = filtered
          this.errors = e
        },
        nextPanel(panel){
          let e = this.errors[panel]
          if(e.length){
            // alert('Errors on '+e+ ' field'+(e > 1 ? 's' : ''))
            console.log(e)
          } else {
            this.step = panel + 1
          }
        }
      }
    }
</script>
