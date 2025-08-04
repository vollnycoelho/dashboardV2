<template>
  <div class="fixed left-0 top-0 w-64 h-full shadow-lg border-r border-gray-200 flex flex-col" style="background-color: #F6FAFC;">
    <!-- Logo Section -->
    <div class="flex items-center justify-between p-6 border-b border-gray-200 flex-shrink-0" style="background-color: #F6FAFC;">
      <!-- Logo -->
      <div class="flex items-center">
        <div class="bg-purple-600 w-8 h-8 rounded-lg flex items-center justify-center mr-3">
          <span class="text-white font-bold text-sm">T</span>
        </div>
        <span class="text-xl font-bold text-gray-800">TurHR</span>
      </div>
      
      <!-- Profile Avatar -->
      <div class="w-8 h-8 bg-gray-400 rounded-full cursor-pointer hover:ring-2 hover:ring-purple-500 hover:ring-offset-2 transition-all duration-150">
        <img 
          src="https://static.vecteezy.com/system/resources/thumbnails/000/439/863/small/Basic_Ui__28186_29.jpg" 
          alt="Profile" 
          class="w-8 h-8 rounded-full object-cover"
        />
      </div>
    </div>

    <!-- Scrollable Navigation Content -->
    <div class="flex-1 overflow-y-auto" style="background-color: #F6FAFC;">
      <nav class="p-6">
        <!-- Main Menu Items -->
        <div class="space-y-1">
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 bg-white hover:bg-gray-50 rounded-lg border border-gray-300">
            <Home class="w-5 h-5 mr-3" />
            <span class="font-bold">Dashboard</span>
          </a>
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-100 rounded-lg">
            <Folder class="w-5 h-5 mr-3" />
            <span class="font-bold">Projects</span>
          </a>
          
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
            <Calendar class="w-5 h-5 mr-3" />
            <span class="font-bold">Calendar</span>
          </a>
          
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
            <Clock class="w-5 h-5 mr-3" />
            <span class="font-bold">Leave Management</span>
          </a>
          
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
            <Settings class="w-5 h-5 mr-3" />
            <span class="font-bold">Settings</span>
          </a>
          
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
            <Bell class="w-5 h-5 mr-3" />
            <span class="font-bold">Notification</span>
          </a>
          
          <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
            <HelpCircle class="w-5 h-5 mr-3" />
            <span class="font-bold">Help & Center</span>
          </a>
        </div>

        <!-- Team Management Section -->
        <div class="mt-8">
          <h3 class="text-xs font-bold text-gray-500 uppercase tracking-wider mb-4 px-4">
            Team Management
          </h3>
          <div class="space-y-1">
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <TrendingUp class="w-5 h-5 mr-3" />
              <span class="font-bold">Performance</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <DollarSign class="w-5 h-5 mr-3" />
              <span class="font-bold">Payrolls</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <FileText class="w-5 h-5 mr-3" />
              <span class="font-bold">Invoices</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <Users class="w-5 h-5 mr-3" />
              <span class="font-bold">Employees</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <UserPlus class="w-5 h-5 mr-3" />
              <span class="font-bold">Recruitment & Hiring</span>
            </a>
          </div>
        </div>

        <!-- List Section -->
        <div class="mt-8">
          <h3 class="text-xs font-bold text-gray-500 uppercase tracking-wider mb-4 px-4">
            <ChevronDown class="w-3 h-3 inline mr-1" />
            List
          </h3>
          <div class="space-y-1">
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <DollarSign class="w-5 h-5 mr-3" />
              <span class="font-bold">Salary Information</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <BarChart3 class="w-5 h-5 mr-3" />
              <span class="font-bold">Compensation Breakdown</span>
            </a>
            
            <a href="#" class="flex items-center px-4 py-3 text-gray-700 hover:bg-gray-200 rounded-lg">
              <Database class="w-5 h-5 mr-3" />
              <span class="font-bold">Project-specific Data</span>
            </a>
          </div>
        </div>

        <!-- Announcements Section -->
        <div class="mt-8 mb-6">
          <div class="bg-white rounded-xl p-4 shadow-sm">
            <!-- Header with icon and title -->
            <div class="flex items-center space-x-3 mb-3">
              <div class="bg-purple-600 w-10 h-10 rounded-full flex items-center justify-center">
                <Bell class="w-5 h-5 text-white" />
              </div>
              <h4 class="font-semibold text-gray-900 text-base">Announcements</h4>
            </div>
            
            <!-- Description text -->
            <div class="mb-4">
              <p class="text-gray-600 text-sm">Stay updated with</p>
              <p class="text-gray-600 text-sm">TurHR</p>
            </div>
            
            <!-- Create Now button -->
            <div class="mb-4">
              <button class="text-purple-600 font-medium text-sm hover:text-purple-700">
                Create Now
              </button>
            </div>
            
            <!-- Read by section -->
            <div class="flex">
              <div class="mr-3">
                <p class="text-gray-600 text-sm">Read</p>
                <p class="text-gray-600 text-sm">by:</p>
              </div>
              <div class="flex -space-x-1 mt-1">
                <img 
                  src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=28&h=28&fit=crop&crop=face" 
                  alt="User" 
                  class="w-7 h-7 rounded-full border-2 border-white object-cover"
                />
                <img 
                  src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=28&h=28&fit=crop&crop=face" 
                  alt="User" 
                  class="w-7 h-7 rounded-full border-2 border-white object-cover"
                />
                <img 
                  src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=28&h=28&fit=crop&crop=face" 
                  alt="User" 
                  class="w-7 h-7 rounded-full border-2 border-white object-cover"
                />
                <div class="w-7 h-7 bg-gray-500 rounded-full border-2 border-white flex items-center justify-center">
                  <span class="text-xs font-medium text-white">+10</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
import { 
  Home, 
  Folder, 
  Calendar, 
  Clock, 
  Settings, 
  Bell, 
  HelpCircle, 
  TrendingUp, 
  DollarSign, 
  FileText, 
  Users, 
  UserPlus, 
  BarChart3, 
  Database,
  ChevronDown
} from 'lucide-vue-next'

export default {
  name: 'Sidebar',
  components: {
    Home,
    Folder,
    Calendar,
    Clock,
    Settings,
    Bell,
    HelpCircle,
    TrendingUp,
    DollarSign,
    FileText,
    Users,
    UserPlus,
    BarChart3,
    Database,
    ChevronDown
  }
}
</script>