<script setup lang="ts">
import SiteFooter from '@/components/SiteFooter.vue'
import SiteHeader from '@/components/SiteHeader.vue'
</script>

<template>
  <SiteHeader />
    <main>
      <RouterView />
    </main>
  <SiteFooter/>
</template>

<style scoped></style>
