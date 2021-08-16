<template>
  <div class="app">
    <div class="app__wrap" v-if="!appReady">
      <div class="spinner">Loading...</div>
    </div>
    <div class="app__wrap" v-if="appReady">
      <form class="" action="/" method="post" autocomplete="off">
        <div class="progress">
          <div class="progress__text">
            Progress: <b>{{ progress }}</b> (Step {{ step +1 }} of {{ panels.length }})
          </div>
          <div class="progress__bubbles">
            <button v-for="(i, index) in panels" :key="index+'_button'"
            type="button" :class="{ active: step == index }" @click="step = index">{{ index +1 }}</button>
          </div>
        </div>
        <main>
          <div v-for="(i, index) in panels" :key="index+'_panel'"
          class="panel" :class="{ before: step > index, active: step == index, after: step < index }">
          <header>
            <h1>{{ i.title }}</h1>
          </header>
          <div class="panel__fields">
            <div v-for="input in i.inputs" :key="input.inputName" class="panel__cell" :class="{'panel__cell--full': (input.width == 2) }">
              <component :is="input.type"
                :label="input.label"
                :inputName="input.inputName"
                :placeholder="input.placeholder"
                :options="input.options"
                :panel="index"
                :flagged="(flags.includes(input.inputName) ? true : false)"
              />
            </div>
          </div>
          <footer>
            <button type="button" @click="nextPanel(index)" class="button">Next</button>
          </footer>
          </div>
          <div class="dev">
            <button class="dev__toggle"
              :state="showDev ? 'active' : ''"
              type="button"
              @click="showDev = !showDev">
            </button>
            <div class="dev__log" v-if="showDev">
              <ul>
                <li v-for="(log, index) in devlog" :key="index+'_log'">
                  {{ log }}
                  <button type="button" @click="deleteDevLog(index)">x</button>
                </li>
              </ul>
              <button class="dev__reset" type="button" @click="devlog = []">Clear All</button>
            </div>
          </div>
        </main>
      </form>
    </div>
  </div>
</template>

<script>
    import('./assets/css/main.css');
    import TextControl from './components/controls/text.vue'
    import RadioControl from './components/controls/radio.vue'
    import CheckboxControl from './components/controls/checkbox.vue'
    import SelectControl from './components/controls/select.vue'
    import EmailControl from './components/controls/text/email.vue'
    import appData from './appData.json'
    export default {
      components: { TextControl, RadioControl, CheckboxControl, SelectControl, EmailControl },
      data () {
        return {
          // Mount
          appReady: false,
          // Steps
          panels: appData.panels,
          step: 0,
          errors: appData.panels.map(function(){ return new Array(0) }),
          flags: [],
          // Dev
          showDev: false,
          devlog: []
        }
      },
      mounted () {
        var self = this
        this.log('App Mounted')
        setTimeout(function(){
          self.appReady = true
        }, 350)
      },
      computed: {
        progress () {
          return ((this.step +1 ) / this.panels.length) * 100 + '%'
        }
      },
      methods: {
        log (data) {
          this.devlog.push(data)
          console.log(data)
        },
        deleteDevLog (index){
          this.devlog.splice(index, 1)
        },
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
            this.flags = e
            this.log('Errors on Fields: '+e)
          } else {
            this.step = panel + 1
            this.flags = []
          }
        }
      }
    }
</script>
