<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-6">
      <h3 class="text-sm font-medium text-gray-600">Attendance Overview</h3>
      <MoreHorizontal class="w-4 h-4 text-gray-400" />
    </div>
    
    <div class="mb-6">
      <div class="flex items-baseline space-x-2">
        <span class="text-3xl font-bold text-gray-900">90%</span>
        <span class="text-sm text-green-500 font-medium">+20% since last month</span>
      </div>
    </div>

    <!-- Progress Bar -->
    <div class="mb-4">
      <div class="flex h-2 bg-gray-200 rounded-full overflow-hidden">
        <div class="w-[15%] bg-yellow-400"></div>
        <div class="w-[25%] bg-teal-400"></div>
        <div class="w-[60%] bg-purple-400"></div>
      </div>
    </div>

    <!-- Legend -->
    <div class="flex items-center justify-start space-x-6 text-xs">
      <div class="flex items-center">
        <div class="w-2 h-2 bg-yellow-400 rounded-full mr-2"></div>
        <span class="text-gray-600">Sick Leave</span>
      </div>
      <div class="flex items-center">
        <div class="w-2 h-2 bg-teal-400 rounded-full mr-2"></div>
        <span class="text-gray-600">Day Off</span>
      </div>
      <div class="flex items-center">
        <div class="w-2 h-2 bg-purple-400 rounded-full mr-2"></div>
        <span class="text-gray-600">On time</span>
      </div>
    </div>
  </div>
</template>

<script>
import { MoreHorizontal } from 'lucide-vue-next'

export default {
  name: 'AttendanceCard',
  components: {
    MoreHorizontal
  }
}
</script>