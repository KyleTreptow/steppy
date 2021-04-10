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
            <TextControl label="First Name" inputName="first_name" placeholder="John" />
            <TextControl label="Last Name" inputName="last_name" placeholder="Doe" />
            <button type="button" @click="step = 2">Next</button>
          </div>
          <div class="panel" :class="{ before: step > 2, active: step == 2, after: step < 2 }">
            <h1>Step 2</h1>
            <RadioControl label="Car Make" inputName="car_make" :options="['Toyota', 'Ford', 'Chevy']" />
            <button type="button" @click="step = 3">Next</button>
          </div>
          <div class="panel" :class="{ before: step > 3, active: step == 3, after: step < 3 }">
            <h1>Step 3</h1>
            <CheckboxControl label="Colors" inputName="colors" :options="['Red', 'Blue', 'Green']" />
            <button type="button" @click="step = 4">Next</button>
          </div>
          <div class="panel" :class="{ before: step > 4, active: step == 4, after: step < 4 }">
            <h1>Step 4</h1>
            <SelectControl label="Shape" inputName="shape" :options="['Square', 'Circle', 'Triangle']" />
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
          step: 1
        }
      }
    }
</script>
