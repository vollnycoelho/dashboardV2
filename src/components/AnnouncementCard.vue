<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-100 p-6 mt-6">
    <div class="flex items-center justify-between">
      <div class="flex items-center">
        <div class="w-10 h-10 bg-purple-100 rounded-full flex items-center justify-center mr-4">
          <MessageSquare class="w-5 h-5 text-purple-600" />
        </div>
        <div>
          <h3 class="text-lg font-semibold text-gray-800">Announcements</h3>
          <p class="text-sm text-gray-500">Stay updated with TurHR</p>
        </div>
      </div>
      <button class="px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700">
        Create Now
      </button>
    </div>
    
    <div class="mt-4 flex items-center">
      <span class="text-sm text-gray-500 mr-2">Read By:</span>
      <div class="flex -space-x-2">
        <div class="w-6 h-6 bg-gray-300 rounded-full border-2 border-white"></div>
        <div class="w-6 h-6 bg-gray-400 rounded-full border-2 border-white"></div>
        <div class="w-6 h-6 bg-gray-500 rounded-full border-2 border-white"></div>
        <div class="w-6 h-6 bg-purple-500 rounded-full border-2 border-white flex items-center justify-center">
          <span class="text-xs text-white font-medium">+10</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { MessageSquare } from 'lucide-vue-next'

export default {
  name: 'AnnouncementCard',
  components: {
    MessageSquare
  }
}
</script>