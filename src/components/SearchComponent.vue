<template>
    <transition name="fade" mode="out-in">
        <div class="search-component" :key="activeTab">
            <div v-if="activeTab === 'Search'">
                <div class="search-field">
                    <input v-model="searchWord1" type="text" placeholder="Enter first search word">
                </div>
                <div class="search-field">
                    <input v-model="searchWord2" type="text" placeholder="Enter second search word">
                </div>
                <div class="timeline">
                    <br />
                    <VueSlider v-model="yearRange" :min="1968" :max="2018" :interval="1" :process="true"
                        :tooltip="'focus'" :tooltip-placement="['top', 'bottom']" :marks="[1968, 1993, 2018]"
                        :enableCross="false" :tooltipStyle="{ 'color': '#000', 'backgroundColor': '#fff' }"
                        :railStyle="{ 'backgroundColor': 'lightgray' }" :processStyle="{ 'backgroundColor': 'black' }">
                    </VueSlider>
                    <br />
                </div>
                <div class="dropdown">
                    <select v-model="selectedPeriod">
                        <option value="calendar">Calendar year</option>
                        <option value="mandate">Mandate period</option>
                        <option value="other">Other</option>
                    </select>
                </div>
                <button @click="search" class="search-button">Search</button>
            </div>

            <div v-else-if="activeTab === 'Me'">
                <button @click="yay" class="yay-button">Yay</button>
            </div>

            <div v-else>
                <!-- Placeholder for other tabs -->
                <p>Search options for {{ activeTab }} tab</p>
            </div>
        </div>
    </transition>
</template>

<script>
import { ref, watch } from 'vue'
import VueSlider from 'vue-3-slider-component'

export default {
    name: 'SearchComponent',
    components: {
        VueSlider
    },
    props: {
        activeTab: {
            type: String,
            required: true
        }
    },
    setup(props, { emit }) {
        const searchWord1 = ref('')
        const searchWord2 = ref('')
        const yearRange = ref([1968, 2018])
        const selectedPeriod = ref('calendar')

        const search = () => {
            emit('search', {
                word1: searchWord1.value,
                word2: searchWord2.value,
                startYear: yearRange.value[0],
                endYear: yearRange.value[1],
                period: selectedPeriod.value
            })
        }

        const yay = () => {
            emit('yay')
        }

        // Reset search fields when tab changes
        watch(() => props.activeTab, () => {
            searchWord1.value = ''
            searchWord2.value = ''
            //yearRange.value = [1968, 2018]
            //selectedPeriod.value = 'calendar'
        })

        return {
            searchWord1,
            searchWord2,
            yearRange,
            selectedPeriod,
            search,
            yay
        }
    }
}
</script>

<style scoped>
.search-component {
    padding: 20px;
}

.search-field {
    margin-bottom: 15px;
}

.search-field input {
    width: 100%;
    padding: 8px;
    border: 1px solid black;
}

.timeline {
    margin: 30px 0;
}

.dropdown {
    margin-bottom: 15px;
}

.dropdown select {
    width: 100%;
    padding: 8px;
    border: 1px solid black;
}

.search-button,
.yay-button {
    width: 100%;
    padding: 10px;
    background-color: white;
    border: 1px solid black;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.search-button:hover,
.yay-button:hover {
    background-color: #f0f0f0;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}
</style>