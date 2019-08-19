<template>
  <div id="app">
    <h2>Vue Autocomplete</h2>
    <switch-theme />
    <p>
      Selected Timezone: <b>{{ selectedTimezone || 'Not chosen'}}</b>
    </p>
    <cool-select v-model="selectedTimezone" :items="items"  item-value="name" item-text="name">
        <template slot="item" slot-scope="{ item : timezone }">
            <div style="display:flex;align-items:center;">
              <img :src="getFlag(timezone.countryCode)" class="country-flag">
                <div>{{ timezone.offset }}<b> {{ timezone.name }}</b></div>
              </div>
        </template>

        <template slot="selection" slot-scope="{ item :timezone }">
              <img :src="getFlag(timezone.countryCode)" class="country-flag">
                <div>{{ timezone.offset }}<b> {{ timezone.name }}</b></div>
              
        </template>
    
    </cool-select>
    <button style="margin-top:15px;" @click="setRandom">
      Set random value
      </button>


   <!-- <span slot="error" slot-scope="{ errorMessage }">
      Error: {{errorMessage}}
    </span>-->
  </div>
</template>
<script>
  import { CoolSelect } from 'vue-cool-select'
  import SwitchTheme from './components/SwitchTheme.vue'
  import countries from "./assets/countries"
  export default {
    name:'App',
    components: {
        CoolSelect,
        SwitchTheme,
      
    },
    data() {
      return {
            selected: null,
            items: countries.data,
            selectedTimezone:'Asia/Jakarta'
            //selectedCountry: 'India'
           // errorMessage: null
      }
    },
    // watch: {
      // selected() {
        // this.validate();
      // }

    // },
    methods: { 
      // validate() {
        // this.errorMessage = !this.selected ? "this is required field!" : null;
      // },
      getFlag (flagName) {
        try{
          return require(`./assets/flags/${flagName.toLowerCase()}.svg`)
        } catch (e) {
          return require('./assets/flags/undefined.svg')
        }
      },
      setRandom() {
        const randomIndex = Math.floor(Math.random()*this.items.length)
        this.selectedTimezone = this.items[randomIndex].name
      }
    }
  }
</script>

<style lang="scss" scoped>
.country-flag {
  max-width:30px;
  margin-right: 10px;
  border: 1px solid #eaecf0;
}

#app {
  height: 100vh;
}

#app > div {
  width: 450px;
}


</style>
























