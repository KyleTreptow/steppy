<template>
    <div class="wrap">
      <form class="" action="/" method="post" autocomplete="off">
        <header>
          <button type="button" :class="{ active: step == 1}" @click="step = 1">1</button>
          <button type="button" :class="{ active: step == 2}" @click="step = 2">2</button>
          <button type="button" :class="{ active: step == 3}" @click="step = 3">3</button>
          <button type="button" :class="{ active: step == 4}" @click="step = 4">4</button>
        </header>
        <main>
          <div class="panel" :class="{ before: step > 1, active: step == 1, after: step < 1 }">
            <h1>Step 1</h1>
            <TextControl label="First Name" inputName="first_name" placeholder="John" panel="1" />
            <TextControl label="Last Name" inputName="last_name" placeholder="Doe" panel="1" />
            <button type="button" @click="step = 2">Next</button>
            <div class="well">Errors: {{ errors[1] }}</div>
          </div>
          <div class="panel" :class="{ before: step > 2, active: step == 2, after: step < 2 }">
            <h1>Step 2</h1>
            <RadioControl label="Car Make" inputName="car_make" :options="['Toyota', 'Ford', 'Chevy']" panel="2" />
            <RadioControl label="School" inputName="school" :options="['CSUN', 'USC', 'UCLA', 'Other']" panel="2" />
            <button type="button" @click="step = 3">Next</button>
            <div class="well">Errors: {{ errors[2] }}</div>
          </div>
          <div class="panel" :class="{ before: step > 3, active: step == 3, after: step < 3 }">
            <h1>Step 3</h1>
            <CheckboxControl label="Colors" inputName="colors" :options="['Red', 'Blue', 'Green']" panel="3" />
            <TextControl label="Nickname" inputName="nickname" placeholder="Chester" panel="3" />
            <button type="button" @click="step = 4">Next</button>
            <div class="well">Errors: {{ errors[3] }}</div>
          </div>
          <div class="panel" :class="{ before: step > 4, active: step == 4, after: step < 4 }">
            <h1>Step 4</h1>
            <SelectControl label="Shape" inputName="shape" :options="['Square', 'Circle', 'Triangle']" panel="4" />
            <div class="well">Errors: {{ errors[4] }}</div>
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
          step: 1,
          errors: {
            1: [], 2: [], 3: [], 4: []
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
