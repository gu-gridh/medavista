<template>
  <div id="app">
    <div class="container">
      <aside class="search-sidebar">
        <SearchComponent :activeTab="activeTab" @search="handleSearch" @yay="handleYay" />
      </aside>
      <main class="main-content">
        <nav class="tabs">
          <button v-for="tab in tabs" :key="tab" @click="activeTab = tab" :class="{ active: activeTab === tab }">
            {{ tab }}
          </button>
        </nav>
        <div class="filters-section" v-if="activeTab != 'Home'">
          <div class="filters-header" @click="toggleFilters">
            Filters
            <span :class="['arrow', { 'down': !filtersOpen, 'up': filtersOpen }]">▼</span>
          </div>
          <transition name="slide">
            <div v-if="filtersOpen" class="filters-content">
              <div class="filter-field">
                <label for="people-filter">People:</label>
                <input id="people-filter" v-model="peopleFilter" type="text" placeholder="Search people...">
              </div>
              <div class="filter-field">
                <label for="party-filter">Party:</label>
                <input id="party-filter" v-model="partyFilter" type="text" placeholder="Search party...">
              </div>
            </div>
          </transition>
        </div>
        <div class="tab-content">
          <component :is="activeTabComponent"></component>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import SearchComponent from './components/SearchComponent.vue'
import SearchTab from './components/SearchTab.vue'
import StatsTab from './components/StatsTab.vue'
import NetworkTab from './components/NetworkTab.vue'
import MeTab from './components/MeTab.vue'
import HomeTab from './components/HomeTab.vue'

export default {
  name: 'App',
  components: {
    SearchComponent,
    SearchTab,
    StatsTab,
    NetworkTab,
    MeTab,
    HomeTab
  },
  setup() {
    const tabs = ['Home', 'Search', 'Stats', 'Network', 'Me']
    const activeTab = ref('Home')
    const filtersOpen = ref(false)
    const peopleFilter = ref('')
    const partyFilter = ref('')

    const activeTabComponent = computed(() => {
      switch (activeTab.value) {
        case 'Home': return HomeTab
        case 'Search': return SearchTab
        case 'Stats': return StatsTab
        case 'Network': return NetworkTab
        case 'Me': return MeTab
        default: return HomeTab
      }
    })

    const toggleFilters = () => {
      filtersOpen.value = !filtersOpen.value
    }

    const handleSearch = (searchData) => {
      console.log('Search data:', searchData)
    }

    const handleYay = () => {
      console.log('Yay!')
    }
    return {
      tabs,
      activeTab,
      activeTabComponent,
      filtersOpen,
      toggleFilters,
      peopleFilter,
      partyFilter,
      handleSearch,
      handleYay
    }
  }
}
</script>

<style scoped>
* {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container {
  display: flex;
  height: 100vh;
}

.search-sidebar {
  width: 300px;
  border-right: 1px solid rgb(0, 0, 0);
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