<template>
  <div class="p-6 bg-white min-h-screen">
    <!-- Header Section -->
    <div class="flex items-center justify-between mb-8">
      <div>
        <h1 class="text-3xl font-bold text-gray-800 mb-2">Good Morning, Turja Sen</h1>
      </div>
      <div class="flex items-center space-x-4">
        <span class="text-gray-600">01 Sep - 15 Sep 2025</span>
        <button class="px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700">
          <Download class="w-4 h-4 inline mr-2" />
          Export Data
        </button>
      </div>
    </div>

    <!-- Top Stats Row -->
    <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
      <!-- Total Employees Card -->
    
      <StatsCard 
        title="Total Employees"
        :value="150"
        :change="50"
        subtitle="Fulltime Employee"
        :secondaryValue="50"
        :secondaryChange="10"
        secondarySubtitle="Freelance Employee"
        icon="users"
      />
  

      <!-- Attendance Card -->
      <AttendanceCard />

      <!-- Today Used Devices Card -->
      <DevicesCard />
    </div>

    <!-- Middle Row -->
    <div class="grid grid-cols-1 lg:grid-cols-2 gap-6 mb-8">
      <!-- Employee Performance Ratings -->
      <PerformanceChart />

      <!-- Income Statistics -->
      <IncomeChart />
    </div>

    <!-- Employee Table -->
    <EmployeeTable />

  </div>
</template>

<script>
import { Download } from 'lucide-vue-next'
import StatsCard from './StatsCard.vue'
import AttendanceCard from './AttendanceCard.vue'
import DevicesCard from './DevicesCard.vue'
import PerformanceChart from './PerformanceChart.vue'
import IncomeChart from './IncomeChart.vue'
import EmployeeTable from './EmployeeTable.vue'
import AnnouncementCard from './AnnouncementCard.vue'

export default {
  name: 'Dashboard',
  components: {
    Download,
    StatsCard,
    AttendanceCard,
    DevicesCard,
    PerformanceChart,
    IncomeChart,
    EmployeeTable,
    AnnouncementCard
  }
}
</script>