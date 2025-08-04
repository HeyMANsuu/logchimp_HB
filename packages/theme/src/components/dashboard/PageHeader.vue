<template>
  <header
    :class="[
      'flex items-center justify-between mb-6 px-3 lg:px-6 py-3.5',
      'border-b border-b-neutral-300/70'
    ]"
  >
    <div class="flex items-center gap-x-3">
      <!-- Toggle button -->
      <button class="md:hidden p-1.5 cursor-pointer hover:bg-neutral-200 rounded-full" @click="dashboard.toggleSidebar">
        <PanelLeftIcon aria-hidden="true" class="size-5 stroke-neutral-700" />
        <span class="sr-only">open sidebar</span>
      </button>

      <slot name="left" />
    </div>

    <slot />

    <slot name="right" />
  </header>
</template>

<script setup lang="ts">
import { PanelLeftIcon } from "lucide-vue";

import { useDashboard } from "../../store/dashboard.ts";
const dashboard = useDashboard();

defineOptions({
  name: "DashboardPageHeader",
});
</script>

<style lang="sass" scoped>
.page-header-content
  display: flex
  align-items: flex-start
  justify-content: space-between
  gap: 1rem
  width: 100%

.page-header-left
  flex: 1
  min-width: 0
  display: flex
  align-items: center

.page-header-title
  margin: 0
  font-size: 1.5rem
  font-weight: 600
  color: var(--color-text-primary)
  line-height: 1.2

.page-header-description
  margin: 0.5rem 0 0 0
  color: var(--color-text-secondary)
  font-size: 0.875rem
  line-height: 1.4

.page-header-actions
  display: flex
  align-items: center
  gap: 0.5rem
  flex-shrink: 0
</style> 