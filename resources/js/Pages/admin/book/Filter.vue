<script setup>
import { ref } from "vue"
import { any } from "vue-types";
import VInput from '@/components/VInput/index.vue';
import VSelect from '@/components/VSelect/index.vue';
import VFilter from '@/components/VFilter/index.vue';

const filter = ref({})
const searchValue = ref("")
const filterCategory = ref()

const props = defineProps({
    additional: any()
})

const applyFilter = () => {
    emit('apply', filter.value)
}

const clearFilter = () => {
    filter.value = ref({})
    filterCategory.value.clearSelected()
    emit('clear', filter.value)
}

const search = () => {
    emit('search', searchValue.value)
}

const emit = defineEmits(['search', 'apply', 'clear'])
</script>

<template>
    <!-- Search -->
    <VInput placeholder="Search by title..." is-prefix v-model="searchValue" @update:model-value="search">
        <template v-slot:icon>
            <span class="absolute inset-y-0 left-0 flex items-center px-2 cursor-pointer">
                <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M5.4375 9.375C7.61212 9.375 9.375 7.61212 9.375 5.4375C9.375 3.26288 7.61212 1.5 5.4375 1.5C3.26288 1.5 1.5 3.26288 1.5 5.4375C1.5 7.61212 3.26288 9.375 5.4375 9.375Z"
                        stroke="#8C8C8C" stroke-linecap="round" stroke-linejoin="round" />
                    <path d="M8.22192 8.22168L10.5 10.4998" stroke="#8C8C8C" stroke-linecap="round"
                        stroke-linejoin="round" />
                </svg>
            </span>
        </template>
    </VInput>
    <!-- Filter Section -->
    <VFilter align="right" @apply="applyFilter" @clear="clearFilter">
        <div class="grid grid-cols-1 gap-3 px-4 pb-4 pt-1.5">
            <div>
                <div class="text-xs font-semibold text-slate-400 uppercase mb-1">Filter by Departemen</div>
                <VSelect placeholder="Select" v-model="filter.filter_category"
                    :options="additional.category_list" :clearable="false" ref="filterCategory" />
            </div>
        </div>
        <div class="grid grid-cols-1 gap-3 px-4 pb-4 pt-1.5">
            <div>
                <div class="text-xs font-semibold text-slate-400 uppercase mb-1">Filter by Fungsi</div>
                <VSelect placeholder="Select" v-model="filter.filter_utility"
                    :options="additional.utility_list" :clearable="false" ref="filterUtility" />
            </div>
        </div>
    </VFilter>
</template>