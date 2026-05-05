<script setup lang="ts">
import { computed, ref } from 'vue'
import { RouterLink, useRoute } from 'vue-router'
import { useBookmarksStore } from '@/stores/bookmarks'
import { useSessionStore } from '@/stores/session'
import { useTheme } from '@/composables/useTheme'

const bookmarksStore = useBookmarksStore()
const sessionStore = useSessionStore()
const { isDark, toggleTheme } = useTheme()
const route = useRoute()
const isMenuOpen = ref(false)

const links = computed(() => [
  { label: 'Home', to: '/' },
  { label: 'Explore', to: '/explore' },
  { label: 'Saved', to: '/bookmarks' },
])

const closeMenu = (): void => {
  isMenuOpen.value = false
}

const toggleMenu = (): void => {
  isMenuOpen.value = !isMenuOpen.value
}
</script>

<template>
  <header
    class="sticky top-0 z-50 border-b border-black/5 bg-white/90 backdrop-blur dark:border-white/10 dark:bg-slate-950/90"
  >
    <div class="container-shell flex items-center justify-between gap-2 py-4">
      <RouterLink to="/" class="flex min-w-0 items-center gap-2" @click="closeMenu">
        <div
          class="flex h-10 w-10 shrink-0 items-center justify-center rounded-2xl bg-emerald-500 text-base font-bold text-white shadow-lg shadow-emerald-500/30"
        >
          RB
        </div>

        <div class="min-w-0">
          <p
            class="text-xs font-semibold uppercase tracking-[0.18em] text-emerald-600 dark:text-emerald-300 sm:text-sm sm:tracking-[0.25em]"
          >
            Recipe Book
          </p>

          <p class="hidden text-xs text-slate-500 dark:text-slate-400 md:block">
            Curated cooking experiences
          </p>
        </div>
      </RouterLink>

      <nav class="hidden items-center gap-2 md:flex">
        <RouterLink
          v-for="link in links"
          :key="link.to"
          :to="link.to"
          class="action-button text-slate-600 hover:bg-slate-100 dark:text-slate-300 dark:hover:bg-slate-800"
          :class="
            route.path === link.to
              ? 'bg-slate-900 text-white dark:bg-white dark:text-slate-900'
              : ''
          "
        >
          {{ link.label }}
        </RouterLink>
      </nav>

      <div class="hidden items-center gap-3 md:flex">
        <button
          class="action-button w-[100px] border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-200"
          @click="toggleTheme"
        >
          {{ isDark ? 'Light' : 'Dark' }}
        </button>

        <RouterLink
          to="/bookmarks"
          class="relative action-button border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-100"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2.4"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="h-5 w-5"
          >
            <path d="M6 3h12a1 1 0 0 1 1 1v17l-7-5-7 5V4a1 1 0 0 1 1-1z" />
          </svg>

          <span
            class="absolute -right-1 -top-1 flex h-5 w-5 items-center justify-center rounded-full bg-red-500 text-[11px] font-bold text-white"
          >
            {{ bookmarksStore.total }}
          </span>
        </RouterLink>

        <RouterLink
          v-if="!sessionStore.isAuthenticated"
          to="/login"
          class="action-button border border-slate-200 bg-white text-slate-700 hover:bg-slate-50 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-100"
        >
          Log In
        </RouterLink>

        <RouterLink
          v-else
          to="/login"
          class="flex items-center gap-3 rounded-full border border-slate-200 bg-white px-2 py-1 transition hover:bg-slate-100 dark:border-slate-800 dark:bg-slate-900 dark:hover:bg-slate-800"
        >
          <img
            :src="sessionStore.user?.avatar"
            alt="Profile"
            class="h-9 w-9 rounded-full object-cover"
          />

          <p class="pr-2 text-sm font-semibold text-slate-700 dark:text-slate-100">
            {{ sessionStore.user?.name }}
          </p>
        </RouterLink>
      </div>

      <div class="flex shrink-0 items-center gap-1.5 md:hidden">
        <button
          class="flex h-10 w-10 items-center justify-center rounded-full border border-slate-200 bg-white text-slate-700 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-200"
          @click="toggleTheme"
        >
          <span class="text-lg">
            {{ isDark ? '🌞' : '🌙' }}
          </span>
        </button>

        <RouterLink
          to="/bookmarks"
          class="relative flex h-10 w-10 items-center justify-center rounded-full border border-slate-200 bg-white text-slate-700 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-100"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2.4"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="h-5 w-5"
          >
            <path d="M6 3h12a1 1 0 0 1 1 1v17l-7-5-7 5V4a1 1 0 0 1 1-1z" />
          </svg>

          <span
            class="absolute -right-1 -top-1 flex h-5 w-5 items-center justify-center rounded-full bg-red-500 text-[11px] font-bold text-white"
          >
            {{ bookmarksStore.total }}
          </span>
        </RouterLink>

        <button
          class="flex h-10 w-10 items-center justify-center rounded-full border border-slate-200 bg-white text-slate-700 dark:border-slate-800 dark:bg-slate-900 dark:text-slate-100"
          @click="toggleMenu"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2.4"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="h-5 w-5"
          >
            <line x1="4" y1="7" x2="20" y2="7" />
            <line x1="4" y1="12" x2="20" y2="12" />
            <line x1="4" y1="17" x2="20" y2="17" />
          </svg>
        </button>
      </div>
    </div>

    <div
      v-if="isMenuOpen"
      class="fixed inset-0 z-40 md:hidden"
      @click.self="closeMenu"
    >
      <div class="absolute inset-x-0 top-[72px] px-4 pb-4">
        <div
          class="rounded-3xl border border-slate-200 bg-white p-3 shadow-2xl dark:border-slate-800 dark:bg-slate-950"
          @click.stop
        >
          <RouterLink
            v-if="!sessionStore.isAuthenticated"
            to="/login"
            class="block rounded-2xl bg-slate-900 px-4 py-3 text-sm font-medium text-white dark:bg-white dark:text-slate-900"
            @click="closeMenu"
          >
            Log In
          </RouterLink>

          <RouterLink
            v-else
            to="/login"
            class="mt-2 flex items-center gap-3 rounded-2xl bg-slate-100 px-4 py-3 dark:bg-slate-800"
            @click="closeMenu"
          >
            <img
              :src="sessionStore.user?.avatar"
              alt="Profile"
              class="h-9 w-9 rounded-full object-cover"
            />

            <p class="font-semibold">
              {{ sessionStore.user?.name }}
            </p>
          </RouterLink>

          <RouterLink
            v-for="link in links"
            :key="link.to"
            :to="link.to"
            class="mt-2 block rounded-2xl px-4 py-3 text-sm font-medium hover:bg-slate-100 dark:hover:bg-slate-800"
            @click="closeMenu"
          >
            {{ link.label }}
          </RouterLink>
        </div>
      </div>
    </div>
  </header>
</template>