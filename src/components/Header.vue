<template>
  <header class="bg-white border-b border-gray-400 px-6 py-4">
    <div class="flex items-center justify-between">
      <!-- Left Side -->
      <div class="flex items-center">
        <h1 class="text-2xl font-semibold text-gray-800">Dashboard</h1>
      </div>

      <!-- Right Side -->
      <div class="flex items-center space-x-4">
        <!-- Search Bar -->
        <div class="relative">
          <Search class="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-4 h-4" />
          <input 
            type="text" 
            placeholder="Quick Search..." 
            class="pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent w-64"
          />
        </div>

        <!-- Icons -->
        <button class="p-2 text-gray-400 hover:text-gray-600 transition-colors">
          <Mail class="w-5 h-5" />
        </button>
        
        <button class="p-2 text-gray-400 hover:text-gray-600 transition-colors">
          <ExternalLink class="w-5 h-5" />
        </button>

        <!-- User Avatars -->
        <div class="flex -space-x-1">
          <!-- Avatar 1 -->
          <div class="relative">
            <img 
              src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-4.0.3&auto=format&fit=crop&w=150&h=150&q=80" 
              alt="User 1" 
              class="w-8 h-8 rounded-full border-2 border-white object-cover hover:z-10 transition-transform hover:scale-105"
            />
            <div class="absolute -bottom-0 -right-0 w-2.5 h-2.5 bg-green-400 border border-white rounded-full"></div>
          </div>

          <!-- Avatar 2 -->
          <div class="relative">
            <img 
              src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=150&h=150&q=80" 
              alt="User 2" 
              class="w-8 h-8 rounded-full border-2 border-white object-cover hover:z-10 transition-transform hover:scale-105"
            />
            <div class="absolute -bottom-0 -right-0 w-2.5 h-2.5 bg-yellow-400 border border-white rounded-full"></div>
          </div>

          <!-- Avatar 3 -->
          <div class="relative">
            <img 
              src="https://images.unsplash.com/photo-1438761681033-6461ffad8d80?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=150&h=150&q=80" 
              alt="User 3" 
              class="w-8 h-8 rounded-full border-2 border-white object-cover hover:z-10 transition-transform hover:scale-105"
            />
            <div class="absolute -bottom-0 -right-0 w-2.5 h-2.5 bg-gray-400 border border-white rounded-full"></div>
          </div>

          <!-- More Users Indicator -->
          <div class="w-8 h-8 bg-gradient-to-br from-purple-500 to-purple-600 rounded-full border-2 border-white flex items-center justify-center hover:z-10 transition-transform hover:scale-105 cursor-pointer">
            <span class="text-xs text-white font-semibold">+10</span>
          </div>
        </div>

        <!-- Invite Button -->
        <button class="flex items-center px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors shadow-sm">
          <UserPlus class="w-4 h-4 mr-2" />
          Invite
        </button>
      </div>
    </div>
  </header>
</template>

<script>
import { Search, Mail, ExternalLink, UserPlus } from 'lucide-vue-next'

export default {
  name: 'Header',
  components: {
    Search,
    Mail,
    ExternalLink,
    UserPlus
  }
}
</script>