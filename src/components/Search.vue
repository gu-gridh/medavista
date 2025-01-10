<template>
   <div>
    <h2>Sökord</h2> <!-- TODO import as a component instead -->
              <v-text-field 
                clearable
                @keyup.enter="addWord" 
                label="Lägg till sökord" 
                variant="outlined" 
                class="input"
                v-model="newWord"
                ></v-text-field>

              <div class="chips">
                <v-chip 
                  v-for="word in words" :key="word" 
                  closable        
                  @click="removeWord(word)" 
                  class="word">{{ word }}
                </v-chip>
              </div>

              <v-select
                label="Tidsperiod"
                :items="periods"
                variant="outlined"
                class="input"
              ></v-select>
              Tidsintervall
              <v-range-slider 
                v-model="years"
                :max="maxYear"
                :min="minYear"
                thumb-label="always"
                step="1"
                class="slider">
              </v-range-slider>
              
              <v-radio-group
                v-model="gender"
                inline
              >
                <v-radio
                  label="Alla"
                  value="all"
                  selected
                ></v-radio>
                <v-radio
                  label="Män"
                  value="men"
                ></v-radio>
                <v-radio
                  label="Kvinnor"
                  value="female"
              ></v-radio>
              </v-radio-group>

              <v-select
                v-model="party"
                :items="parties"
                label="Välj parti(er)"
                multiple
                persistent-hint
              ></v-select>

              <v-btn @click="search" color="primary">Sök</v-btn>
   </div>
</template>

<script setup lang="ts">
import { ref, watch } from 'vue'

const newWord = ref('')
const words = ref<string[]>([])
const periods = ref<string[]>(['Riksdagsår', 'Mandatperiod', 'Terrorfaser', ])
const minYear = ref(1967) 
const maxYear = ref(2018)
const years = ref([minYear.value, maxYear.value])
const gender = ref('all')
const party = ref<string[]>([])
//swedish parties in the riksdag since 1967
const parties = ref<string[]>(['Sverigedemokraterna', 'Feministiskt initiativ', 'Miljöpartiet', 'Kristdemokraterna', 'Vänsterpartiet', 'Folkpartiet', 'Centerpartiet', 'Moderaterna', 'Socialdemokraterna', 'Ny Demokrati', 'Junilistan']) //TODO add the rest and sort order

const addWord = () => {
  if (newWord.value) {
    words.value.push(newWord.value)
    newWord.value = ''
  }
}

const removeWord = (word: string) => {
  words.value = words.value.filter(w => w !== word)
}

const search = () => {
  console.log('searching...')
}

</script>

<style scoped>
.input {
  margin-top: 20px;
}

.word {
  margin: 5px;
}

.slider {
  margin: 20px;
  padding-top: 10px;
}

.v-slider-thumb__label {
  color: black !important;
}
</style>