<template>
  <header 
    :class="[
      'form-header',
      'flex items-center justify-between mb-6 px-3 lg:px-6 py-3.5',
      'border-b border-b-neutral-300/70'
    ]" 
    data-test="page-header"
  >
    <div class="page-header-content">
      <div class="page-header-left">
        <!-- Toggle button for mobile -->
        <button 
          class="md:hidden p-1.5 cursor-pointer hover:bg-neutral-200 rounded-full mr-3" 
          @click="dashboard.toggleSidebar"
        >
          <PanelLeftIcon aria-hidden="true" class="size-5 stroke-neutral-700" />
          <span class="sr-only">open sidebar</span>
        </button>

        <breadcrumbs v-if="breadcrumbs && breadcrumbs.length > 0" data-test="page-header-breadcrumbs">
          <h5 
            v-for="(crumb, index) in breadcrumbs" 
            :key="index"
            class="breadcrum-item"
            data-test="page-header-breadcrumb"
          >
            {{ crumb }}
          </h5>
        </breadcrumbs>
        <h1 v-if="title" class="page-header-title" data-test="page-header-title">
          {{ title }}
        </h1>
        <p v-if="description" class="page-header-description" data-test="page-header-description">
          {{ description }}
        </p>
      </div>
      <div v-if="$slots.actions" class="page-header-actions" data-test="page-header-actions">
        <slot name="actions" />
      </div>
    </div>
  </header>
</template>

<script setup lang="ts">
// components
import Breadcrumbs from "../Breadcrumbs.vue";
import { PanelLeftIcon } from "lucide-vue";
import { useDashboard } from "../../store/dashboard.ts";

const dashboard = useDashboard();

interface Props {
  title?: string;
  description?: string;
  breadcrumbs?: string[];
}

defineProps<Props>();

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