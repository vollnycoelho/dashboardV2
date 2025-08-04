<template>
  <div class="min-h-screen bg-gray-50 flex">
    <!-- Sidebar -->
    <Sidebar />
    
    <!-- Main Content -->
    <div class="flex-1 ml-64">
      <Header />
      <Dashboard />
    </div>
  </div>
</template>

<script>
import Sidebar from './components/Sidebar.vue'
import Header from './components/Header.vue'
import Dashboard from './components/Dashboard.vue'

export default {
  name: 'App',
  components: {
    Sidebar,
    Header,
    Dashboard
  }
}
</script>