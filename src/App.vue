<template>
   <v-app id="medavista" :theme="theme">

      <!-- Top navigation bar -->
      <v-app-bar :elevation="2" app>
        <v-toolbar-title>SweTerror-portalen</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn>Exempel</v-btn>
        <v-btn>Om</v-btn>
        <v-btn
          :prepend-icon="theme === 'light' ? 'mdi-weather-sunny' : 'mdi-weather-night'"
          slim
          @click="onClick"
        ></v-btn>
      </v-app-bar>

      <v-container class="main-container" >
        <!-- Navigation Drawer -->
        <v-navigation-drawer permanent class="drawer" :width="400">
          <SearchComponent />
        </v-navigation-drawer>

        <v-container class="inner-nav">
              <!-- <v-tabs>
              <v-tab>INTRO</v-tab>
              <v-tab>Tab 2</v-tab>
              <v-tab>Tab 3</v-tab>
            </v-tabs> -->
            <v-app-bar class="results-tabs" elevation="1" app>
              <!-- <v-toolbar-title>Analysresultat</v-toolbar-title> -->
              <v-btn>Semantisk analys</v-btn>
              <v-btn>Frekvens & trender</v-btn>
              <v-btn>Entiteter & Nätverk</v-btn>
              <v-btn>Politisk analys</v-btn>
            </v-app-bar>
            </v-container>
          <v-main>
          <v-container class="main-view">  
            <RouterView />
          </v-container>
        </v-main>
        </v-container>
<Footer/>
  </v-app>
</template>


<script setup lang="ts">
import { ref } from 'vue'
import SearchComponent from './components/Search.vue'
import Footer from './components/Footer.vue'

const theme = ref('dark')

const onClick = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

</script>

<style scoped>

* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0; /* Ensure no global margins */
  padding: 0;
  box-sizing: border-box; /* Prevent overflow issues */
}

.drawer {
  padding: 20px;
  height: fit-content;
  margin-top: 20px;
  margin-left: 20px;
  border-radius: 10px;
}

.main-container {
  flex-grow: 1;
  padding: 20px;
  margin-left: 420px;
  margin-top: 80px;
}


.inner-nav {
  
  padding-bottom: 20px;
  padding-right: 20px;
}

.main-viev {
  min-width: 100vw;
  display: flex;
  padding: 20px;
}

.results-tabs {
  margin-top: 20px;
  margin-right: 20px;
  padding: 0px 10px;
  border-radius: 10px;
}

.results-tabs button {
  margin-right: 30px;
}
</style>