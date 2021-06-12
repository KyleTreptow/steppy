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
    export default {
      components: { TextControl, RadioControl, CheckboxControl, SelectControl },
      data () {
        return {
          panels: [
            {
              title: 'step 1',
              inputs: [
                {
                  type: 'TextControl',
                  label: 'First Name',
                  inputName: 'first_name',
                  placeholder: 'John'
                },
                {
                  type: 'TextControl',
                  label: 'Last Name',
                  inputName: 'last_name',
                  placeholder: 'Doe'
                }
              ]
            },
            {
              title: 'step 2',
              inputs: [
                {
                  type: 'RadioControl',
                  label: 'Car Make',
                  inputName: 'car_name',
                  options: ['Toyota', 'Ford', 'Chevy']
                },
                {
                  type: 'RadioControl',
                  label: 'School',
                  inputName: 'school',
                  options: ['CSUN', 'USC', 'UCLA', 'Other']
                }
              ]
            },
            {
              title: 'step 3',
              inputs: [
                {
                  type: 'CheckboxControl',
                  label: 'Colors',
                  inputName: 'colors',
                  options: ['Red', 'Blue', 'Green']
                },
                {
                  type: 'TextControl',
                  label: 'Nickname',
                  inputName: 'nickname',
                  placeholder: 'Chester'
                }
              ]
            },
            {
              title: 'step 4',
              inputs: [
                {
                  type: 'SelectControl',
                  label: 'Shape',
                  inputName: 'shape',
                  options: ['Square', 'Circle', 'Triangle']
                },
              ]
            }
          ],
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
          }
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
