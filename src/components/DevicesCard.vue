<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-6">
      <h3 class="text-sm font-medium text-gray-600">Today Used Devices</h3>
      <MoreHorizontal class="w-4 h-4 text-gray-400" />
    </div>
    
    <div class="flex items-center space-x-6">
      <!-- Circular Progress -->
      <div class="relative">
        <div class="w-20 h-20">
          <svg class="w-20 h-20 transform -rotate-90" viewBox="0 0 36 36">
            <!-- Background circle -->
            <path class="text-gray-200" stroke="currentColor" stroke-width="2.5" fill="none" 
                  d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"/>
            <!-- Purple segment -->
            <path class="text-purple-500" stroke="currentColor" stroke-width="2.5" fill="none" stroke-linecap="round"
                  stroke-dasharray="70, 100" stroke-dashoffset="0"
                  d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"/>
            <!-- Orange segment -->
            <path class="text-orange-400" stroke="currentColor" stroke-width="2.5" fill="none" stroke-linecap="round"
                  stroke-dasharray="15, 100" stroke-dashoffset="-70"
                  d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"/>
          </svg>
          <div class="absolute inset-0 flex items-center justify-center">
            <div class="text-center">
              <div class="text-lg font-bold text-gray-900">100</div>
              <div class="text-xs text-gray-500">Overall</div>
            </div>
          </div>
        </div>
      </div>

      <!-- Device Stats -->
      <div class="flex-1 space-y-2">
        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <div class="w-2 h-2 bg-purple-500 rounded-full mr-2"></div>
            <span class="text-sm text-gray-600">Macbook</span>
          </div>
          <span class="text-sm font-semibold text-gray-900">80</span>
        </div>
        
        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <div class="w-2 h-2 bg-orange-400 rounded-full mr-2"></div>
            <span class="text-sm text-gray-600">Keyboard</span>
          </div>
          <span class="text-sm font-semibold text-gray-900">13</span>
        </div>
        
        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <div class="w-2 h-2 bg-gray-300 rounded-full mr-2"></div>
            <span class="text-sm text-gray-600">Headphones</span>
          </div>
          <span class="text-sm font-semibold text-gray-900">07</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { MoreHorizontal } from 'lucide-vue-next'

export default {
  name: 'DevicesCard',
  components: {
    MoreHorizontal
  }
}
</script>