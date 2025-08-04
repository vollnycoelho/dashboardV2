<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-sm font-medium text-gray-600">{{ title }}</h3>
      <MoreHorizontal class="w-4 h-4 text-gray-400" />
    </div>
    
    <div class="space-y-6">
      <!-- Main Stat -->
      <div class="bg-blue-50 rounded-lg p-4">
        <div class="flex items-baseline space-x-2 mb-1">
          <span class="text-2xl font-bold text-gray-900">{{ value }}</span>
          <span class="text-sm text-green-500 font-medium">+{{ change }}</span>
        </div>
        <p class="text-sm text-green-500">{{ subtitle }}</p>
      </div>

      <!-- Secondary Stat -->
      <div class="bg-orange-50 rounded-lg p-4">
        <div class="flex items-baseline space-x-2 mb-1">
          <span class="text-2xl font-bold text-gray-900">{{ secondaryValue }}</span>
          <span class="text-sm text-orange-500 font-medium">+{{ secondaryChange }}</span>
        </div>
        <p class="text-sm text-orange-500">{{ secondarySubtitle }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import { MoreHorizontal } from 'lucide-vue-next'

export default {
  name: 'StatsCard',
  components: {
    MoreHorizontal
  },
  props: {
    title: {
      type: String,
      default: 'Total Employees'
    },
    value: {
      type: Number,
      default: 150
    },
    change: {
      type: Number,
      default: 50
    },
    subtitle: {
      type: String,
      default: 'Fulltime Employee'
    },
    secondaryValue: {
      type: Number,
      default: 50
    },
    secondaryChange: {
      type: Number,
      default: 10
    },
    secondarySubtitle: {
      type: String,
      default: 'Freelance Employee'
    }
  }
}
</script>