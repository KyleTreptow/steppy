<template>
    <div class="wrap">
      <form class="" action="/" method="post" autocomplete="off">
        <header>
          <button v-for="(i, index) in panels" :key="index+'_button'"
          type="button" :class="{ active: step == index }" @click="step = index">{{ index + 1 }}</button>
        </header>
        <main>
          <div v-for="(i, index) in panels" :key="index+'_panel'"
          class="panel" :class="{ before: step > index, active: step == index, after: step < index }">
            <h1>{{ i.title }}</h1>
            <div v-for="input in i.inputs" :key="input.inputName">
              <component :is="input.type"
                :label="input.label"
                :inputName="input.inputName"
                :placeholder="input.placeholder"
                :options="input.options"
                :panel="index"
              />
            </div>
            <button type="button" @click="step = index+1">Next</button>
            <div class="well">Errors: {{ errors[index] }}</div>
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
          errors: {
            0: [], 1: [], 2: [], 3: []
          }
        }
      },
      methods: {
        addErrorFlag (flag, panel) {
          if(!this.errors[panel].includes(flag)){
            this.errors[panel].push(flag)
          }a
        },
        removeErrorFlag (flag, panel) {
          let filtered = this.errors[panel].filter(function(value){
            return value != flag;
          })
          this.errors[panel] = filtered
        }
      }
    }
</script>
