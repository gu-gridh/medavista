<template>
    <v-app id="medavista" theme="dark">
      <v-layout fluid>
      <v-theme-provider theme="dark"> <!-- can be changed https://vuetifyjs.com/en/features/theme/#changing-theme -->
        <v-app-bar :elevation="2">
          <v-toolbar-title>SweTerror-portalen</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn>Exempel</v-btn>
          <v-btn>Om </v-btn>
        </v-app-bar>

        <v-main class="d-flex main-content">
          <v-container class="main-container">
            <!-- left search drawer -->
            <v-navigation-drawer permanent class="drawer" :width="400"> <!-- TODO responsive -->
              <SearchComponent />
            </v-navigation-drawer>
            <div>Inner search bar</div>
            <!-- Search content etc -->
            <div>
              <RouterView />
            </div>
          </v-container>
        </v-main>

      </v-theme-provider>
      </v-layout>
    </v-app>
</template>


<script setup lang="ts">
import { ref } from 'vue'
import SearchComponent from './components/Search.vue'


</script>

<style scoped>
* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.drawer {
  padding: 20px;
  margin: 20px;
  border-radius: 10px;
}



.main-container {
  margin-left: 32px;
}

.main-content {
  flex-grow: 1;
  display: flex;
  flex-direction: column;
}


</style>