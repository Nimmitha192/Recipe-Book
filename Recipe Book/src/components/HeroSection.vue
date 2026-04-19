<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>

<template>
  <section class="container-shell grid gap-8 py-10 lg:grid-cols-[1.2fr_0.8fr] lg:py-16">
    <div class="surface-card overflow-hidden p-8 lg:p-12">
      <span class="tag-pill">Modern cooking, beautifully organized</span>
      <h1 class="mt-6 max-w-2xl text-4xl font-semibold tracking-tight text-slate-900 sm:text-5xl dark:text-white">
        Discover elevated recipes for everyday meals and weekend hosting.
      </h1>
      <p class="mt-5 max-w-xl text-base leading-7 text-slate-600 dark:text-slate-300">
        Explore globally inspired dishes, save your favorites, and move from inspiration to dinner with a fast, elegant interface.
      </p>
      <div class="mt-8 flex flex-wrap gap-3">
        <RouterLink to="/explore" class="action-button bg-slate-900 text-white hover:bg-slate-700 dark:bg-white dark:text-slate-900 dark:hover:bg-slate-200">
          Browse recipes
        </RouterLink>
        <RouterLink to="/bookmarks" class="action-button border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-100">
          View saved picks
        </RouterLink>
      </div>
      <div class="mt-10 grid gap-4 sm:grid-cols-3">
        <div class="rounded-2xl bg-slate-50 p-4 dark:bg-slate-800/70">
          <p class="text-2xl font-semibold">30+</p>
          <p class="mt-1 text-sm text-slate-500 dark:text-slate-400">Curated recipes</p>
        </div>
        <div class="rounded-2xl bg-slate-50 p-4 dark:bg-slate-800/70">
          <p class="text-2xl font-semibold">Fast</p>
          <p class="mt-1 text-sm text-slate-500 dark:text-slate-400">Dynamic filtering</p>
        </div>
        <div class="rounded-2xl bg-slate-50 p-4 dark:bg-slate-800/70">
          <p class="text-2xl font-semibold">Personal</p>
          <p class="mt-1 text-sm text-slate-500 dark:text-slate-400">Saved recipe collection</p>
        </div>
      </div>
    </div>

    <div class="grid gap-4">
      <div class="surface-card p-6">
        <img src="https://images.unsplash.com/photo-1490645935967-10de6ba17061?auto=format&fit=crop&w=1200&q=80" alt="Styled food table" class="h-72 w-full rounded-[2rem] object-cover" />
      </div>
      <div class="grid gap-4 sm:grid-cols-2">
        <div class="surface-card p-6">
          <p class="text-sm font-semibold uppercase tracking-[0.2em] text-slate-500 dark:text-slate-400">Thoughtful details</p>
          <p class="mt-3 text-lg font-semibold">Cuisine tags, meal type filters, and polished detail pages.</p>
        </div>
        <div class="surface-card p-6">
          <p class="text-sm font-semibold uppercase tracking-[0.2em] text-slate-500 dark:text-slate-400">Save favorites</p>
          <p class="mt-3 text-lg font-semibold">Bookmarks persist across reloads for a real product feel.</p>
        </div>
      </div>
    </div>
  </section>
</template>
