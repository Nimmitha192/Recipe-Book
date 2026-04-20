<script setup lang="ts">
import { computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import { useRecipesStore } from '@/stores/recipes'
import { useBookmarksStore } from '@/stores/bookmarks'

const route = useRoute()
const recipesStore = useRecipesStore()
const bookmarksStore = useBookmarksStore()

onMounted(async () => {
  await recipesStore.fetchRecipes()
})

const recipeId = computed(() => Number(route.params.id))
const recipe = computed(() => recipesStore.recipes.find((item) => item.id === recipeId.value) ?? null)
</script>

<template>
  <section class="container-shell py-10" v-if="recipe">
    <div class="grid gap-8 lg:grid-cols-[1.05fr_0.95fr]">
      <div class="surface-card overflow-hidden p-4 sm:p-6">
        <img :src="recipe.image" :alt="recipe.name" class="h-[360px] w-full rounded-[2rem] object-cover sm:h-[480px]" />
      </div>

      <div class="surface-card p-8">
        <div class="flex flex-wrap gap-2">
          <span class="tag-pill">{{ recipe.cuisine }}</span>
          <span class="tag-pill" v-for="tag in recipe.tags.slice(0, 3)" :key="tag">{{ tag }}</span>
        </div>
        <h1 class="mt-5 text-4xl font-semibold">{{ recipe.name }}</h1>
        <p class="mt-4 text-base leading-7 text-slate-600 dark:text-slate-300">
          A refined {{ recipe.mealType.join(', ').toLowerCase() }} option with {{ recipe.difficulty.toLowerCase() }} difficulty and strong community feedback.
        </p>

        <div class="mt-6 grid gap-4 sm:grid-cols-2">
          <div class="rounded-3xl bg-slate-50 p-4 dark:bg-slate-800/70"><p class="text-sm text-slate-500 dark:text-slate-400">Prep time</p><p class="mt-1 text-xl font-semibold">{{ recipe.prepTimeMinutes }} mins</p></div>
          <div class="rounded-3xl bg-slate-50 p-4 dark:bg-slate-800/70"><p class="text-sm text-slate-500 dark:text-slate-400">Cook time</p><p class="mt-1 text-xl font-semibold">{{ recipe.cookTimeMinutes }} mins</p></div>
          <div class="rounded-3xl bg-slate-50 p-4 dark:bg-slate-800/70"><p class="text-sm text-slate-500 dark:text-slate-400">Servings</p><p class="mt-1 text-xl font-semibold">{{ recipe.servings }}</p></div>
          <div class="rounded-3xl bg-slate-50 p-4 dark:bg-slate-800/70"><p class="text-sm text-slate-500 dark:text-slate-400">Rating</p><p class="mt-1 text-xl font-semibold">★ {{ recipe.rating.toFixed(1) }}</p></div>
        </div>

        <button class="mt-8 action-button bg-amber-400 text-slate-900 hover:bg-amber-300" @click="bookmarksStore.toggle(recipe)">
          {{ bookmarksStore.isBookmarked(recipe.id) ? 'Remove from saved' : 'Save this recipe' }}
        </button>
      </div>
    </div>

    <div class="mt-8 grid gap-8 lg:grid-cols-2">
      <div class="surface-card p-8">
        <p class="text-sm font-semibold uppercase tracking-[0.2em] text-slate-500 dark:text-slate-400">Ingredients</p>
        <ul class="mt-5 space-y-3 text-sm leading-7 text-slate-700 dark:text-slate-200">
          <li v-for="ingredient in recipe.ingredients" :key="ingredient" class="rounded-2xl bg-slate-50 px-4 py-3 dark:bg-slate-800/70">{{ ingredient }}</li>
        </ul>
      </div>

      <div class="surface-card p-8">
        <p class="text-sm font-semibold uppercase tracking-[0.2em] text-slate-500 dark:text-slate-400">Method</p>
        <ol class="mt-5 space-y-4">
          <li v-for="(step, index) in recipe.instructions" :key="`${recipe.id}-${index}`" class="flex gap-4">
            <span class="flex h-9 w-9 shrink-0 items-center justify-center rounded-full bg-slate-900 text-sm font-semibold text-white dark:bg-white dark:text-slate-900">{{ index + 1 }}</span>
            <p class="pt-1 text-sm leading-7 text-slate-700 dark:text-slate-200">{{ step }}</p>
          </li>
        </ol>
      </div>
    </div>
  </section>

  <section v-else class="container-shell py-16">
    <div class="surface-card p-10 text-center">
      <p class="text-lg font-semibold">Recipe not found.</p>
    </div>
  </section>
</template>
