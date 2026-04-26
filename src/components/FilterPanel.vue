<script setup lang="ts">
const props = defineProps<{
  search: string
  cuisines: string[]
  mealTypes: string[]
  selectedCuisine: string
  selectedMealType: string
}>()

const emit = defineEmits<{
  search: [value: string]
  cuisine: [value: string]
  mealType: [value: string]
}>()

const handleSearch = (event: Event) => {
  emit('search', (event.target as HTMLInputElement).value)
}

const handleCuisineChange = (event: Event) => {
  emit('cuisine', (event.target as HTMLSelectElement).value)
}

const handleMealTypeChange = (event: Event) => {
  emit('mealType', (event.target as HTMLSelectElement).value)
}
</script>

<template>
  <section class="surface-card p-5">
    <div class="grid gap-4 lg:grid-cols-[1.4fr_1fr_1fr]">
      <label class="block">
        <span class="mb-2 block text-sm font-medium text-slate-700 dark:text-slate-200">
          Search recipes
        </span>
        <input
          :value="props.search"
          type="text"
          placeholder="Search by name, ingredient, or tag"
          class="w-full rounded-2xl border border-slate-200 bg-white px-4 py-3 text-sm outline-none ring-0 transition focus:border-emerald-400 dark:border-slate-800 dark:bg-slate-950"
          @input="handleSearch"
        />
      </label>

      <label class="block">
        <span class="mb-2 block text-sm font-medium text-slate-700 dark:text-slate-200">
          Cuisine
        </span>
        <select
          :value="props.selectedCuisine"
          class="w-full rounded-2xl border border-slate-200 bg-white px-4 py-3 text-sm outline-none transition focus:border-emerald-400 dark:border-slate-800 dark:bg-slate-950"
          @change="handleCuisineChange"
        >
          <option
            v-for="cuisine in props.cuisines"
            :key="cuisine"
            :value="cuisine"
          >
            {{ cuisine }}
          </option>
        </select>
      </label>

      <label class="block">
        <span class="mb-2 block text-sm font-medium text-slate-700 dark:text-slate-200">
          Meal type
        </span>
        <select
          :value="props.selectedMealType"
          class="w-full rounded-2xl border border-slate-200 bg-white px-4 py-3 text-sm outline-none transition focus:border-emerald-400 dark:border-slate-800 dark:bg-slate-950"
          @change="handleMealTypeChange"
        >
          <option
            v-for="mealType in props.mealTypes"
            :key="mealType"
            :value="mealType"
          >
            {{ mealType }}
          </option>
        </select>
      </label>
    </div>
  </section>
</template>