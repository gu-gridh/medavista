<template>
  <div id="app">
    <v-app id="medavista">
      <v-theme-provider theme="dark"> <!-- can be changed https://vuetifyjs.com/en/features/theme/#changing-theme -->
      <v-app-bar app  :elevation="2">
        <v-toolbar-title>SweTerror-portalen</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn>Exempel</v-btn>
        <v-btn>Om </v-btn>
      </v-app-bar>

      <!-- left search drawer -->
      <v-navigation-drawer permanent class="drawer" :width="300"> <!-- TODO responsive -->
        <h2>Sökord</h2>
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
      </v-navigation-drawer>
      </v-theme-provider>
    </v-app>

  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue'

const newWord = ref('')
const words = ref<string[]>([])

const addWord = () => {
  if (newWord.value) {
    words.value.push(newWord.value)
    newWord.value = ''
  }
}

const removeWord = (word: string) => {
  words.value = words.value.filter(w => w !== word)
}

</script>

<style scoped>
* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.drawer {
  padding: 20px;
  margin: 20px;
  height: fit-content;
  border-radius: 10px;
}

.input {
  padding-top: 20px;
}

.word {
  margin: 5px;
}

.container {
  display: flex;
  height: 100vh;
  
}
.main-content {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}

.tabs {
  display: flex;
  border-bottom: 1px solid black;
}

.tabs button {
  background: none;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 16px;
}

.tabs button.active {
  border-bottom: 2px solid black;
}

.filters-section {
  border-bottom: 1px solid black;
}

.filters-header {
  padding: 10px 20px;
  cursor: pointer;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.arrow {
  transition: transform 0.3s ease;
}

.arrow.up {
  transform: rotate(180deg);
}

.filters-content {
  padding: 20px;
}

.filter-field {
  margin-bottom: 10px;
}

.filter-field label {
  display: block;
  margin-bottom: 5px;
}

.filter-field input {
  width: 100%;
  padding: 5px;
  border: 1px solid black;
}

.tab-content {
  flex-grow: 1;
  padding: 20px;
}

.slide-enter-active,
.slide-leave-active {
  transition: max-height 0.5s ease-in-out, opacity 0.5s ease-in-out;
  max-height: 200px;
  overflow: hidden;
}

.slide-enter-from,
.slide-leave-to {
  max-height: 0;
  opacity: 0;
}
</style>