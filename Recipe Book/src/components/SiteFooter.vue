<template>
  <footer class="border-t border-slate-200 bg-white text-slate-900 dark:border-slate-800 dark:bg-slate-950 dark:text-white">
    <div class="w-full">
      <div class="flex flex-col items-center justify-center px-6 py-10 sm:px-8 lg:px-12">
        <div>
          <h2 class="text-center text-3xl font-bold sm:text-4xl lg:text-5xl">
            Recipe Book
          </h2>

          <p class="mt-6 max-w-[600px] pb-[25px] text-center text-sm text-slate-600 sm:text-base dark:text-slate-300">
            Discover, cook, and share delicious recipes from around the world with Recipe Book.
          </p>
        </div>

        <div class="flex flex-wrap items-center justify-center gap-6 sm:gap-8 lg:gap-10">
          <a
            v-for="item in socialLinks"
            :key="item.name"
            :href="item.href"
            class="flex h-10 w-10 items-center justify-center rounded-full border border-slate-200 bg-slate-100 text-slate-800 transition hover:scale-110 hover:bg-slate-200 dark:border-slate-700 dark:bg-slate-800 dark:text-white dark:hover:bg-slate-700"
          >
            <component :is="item.icon" class="h-6 w-6" />
          </a>
        </div>

        <ul class="mt-6 flex flex-wrap items-center justify-center gap-x-6 gap-y-4 text-sm text-slate-600 sm:gap-x-10 sm:text-base dark:text-slate-300">
          <li v-for="link in navLinks" :key="link.name">
            <a :href="link.href" class="transition hover:text-slate-900 dark:hover:text-white">
              {{ link.name }}
            </a>
          </li>
        </ul>
      </div>

      <div class="border-t border-slate-200 py-5 text-center text-sm text-slate-600 dark:border-slate-800 dark:text-slate-300">
        Copyright ©2026; Designed by
        <span class="font-semibold text-slate-900 dark:text-white">Nimmitha</span>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import type { Component } from 'vue'
import {
  Facebook,
  Instagram,
  Twitter,
  Youtube,
  BadgePlus,
} from 'lucide-vue-next'

interface SocialLink {
  name: string
  href: string
  icon: Component
}

interface NavLink {
  name: string
  href: string
}

const socialLinks: SocialLink[] = [
  { name: 'Facebook', href: '#', icon: Facebook },
  { name: 'Instagram', href: '#', icon: Instagram },
  { name: 'Twitter', href: '#', icon: Twitter },
  { name: 'Google', href: '#', icon: BadgePlus },
  { name: 'YouTube', href: '#', icon: Youtube },
]

const navLinks: NavLink[] = [
  { name: 'Home', href: '#' },
  { name: 'Explore', href: '#' },
  { name: 'About', href: '#' },
  { name: 'Contact Us', href: '#' },
  { name: 'Our Team', href: '#' },
]
</script>