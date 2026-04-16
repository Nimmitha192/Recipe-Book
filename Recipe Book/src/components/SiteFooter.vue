<template>
  <footer class="bg-black text-white">
    <div class="w-full">
      
      <!-- Main content -->
      <div class="flex flex-col items-center justify-center px-6 py-10">
        <div class="lg:col-span-5">
          <h2 class="text-5xl text-center font-bold">Recipe Book</h2>

          <p class="mt-6 text-gray-300 max-w-[600px] text-center pb-[25px]">
           Discover, cook, and share delicious recipes from around the world with Recipe Book.
          </p>
        </div>
        
        <!-- Social icons -->
        <div class="flex flex-wrap items-center justify-center gap-10">
          <a
            v-for="item in socialLinks"
            :key="item.name"
            :href="item.href"
            class="flex h-10 w-10 items-center justify-center rounded-full bg-white text-black transition hover:scale-110 hover:bg-gray-200"
          >
            <component :is="item.icon" class="h-7 w-7" />
          </a>
        </div>

        <!-- Navigation -->
        <ul class="mt-6 flex flex-wrap items-center justify-center gap-x-10 gap-y-4 text-md text-gray-300">
          <li v-for="link in navLinks" :key="link.name">
            <a href="#" class="hover:text-white transition">
              {{ link.name }}
            </a>
          </li>
        </ul>

      </div>

      <!-- Bottom bar -->
      <div class="bg-black border-t border-gray-700 py-5 text-center text-gray-300">
        Copyright ©2026; Designed by
        <span class="font-semibold text-white">Nimmitha</span>
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