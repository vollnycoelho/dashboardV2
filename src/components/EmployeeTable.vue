<template>
  <div class="bg-white rounded-lg p-4 shadow-sm border border-gray-200">
    <!-- Header Section -->
    <div class="flex justify-between items-center mb-4">
      <h6 class="text-lg font-semibold text-gray-900 mb-0">All Employees</h6>
      <div class="flex gap-2">
        <input 
          class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent" 
          type="text" 
          placeholder="🔍 Search Employee" 
        />
        <select class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent">
          <option>All Status</option>
          <option>Full-time</option>
          <option>Freelance</option>
        </select>
        <select class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent">
          <option>All Role</option>
        </select>
        <button class="px-3 py-2 text-sm border border-gray-300 text-gray-700 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-purple-500">
          ⭳ Export
        </button>
      </div>
    </div>

    <!-- Table -->
    <div class="overflow-x-auto">
      <table class="w-full table-auto">
        <thead class="bg-gray-50 border-b border-gray-200">
          <tr>
            <th class="px-4 py-3 text-left">
              <input 
                type="checkbox" 
                class="w-4 h-4 text-purple-600 border-gray-300 rounded focus:ring-purple-500"
              />
            </th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Employee ID</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Employee name</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Email</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Role</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Departments</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Status</th>
            <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">Action</th>
          </tr>
        </thead>
        <tbody class="divide-y divide-gray-200">
          <tr v-for="emp in employees" :key="emp.id" class="hover:bg-gray-50">
            <td class="px-4 py-3">
              <input 
                type="checkbox" 
                class="w-4 h-4 text-purple-600 border-gray-300 rounded focus:ring-purple-500"
              />
            </td>
            <td class="px-4 py-3 text-sm text-gray-900">{{ emp.id }}</td>
            <td class="px-4 py-3">
              <div class="flex items-center gap-3">
                <img 
                  :src="emp.avatar" 
                  class="w-8 h-8 rounded-full object-cover" 
                  :alt="emp.name"
                />
                <span class="text-sm font-medium text-gray-900">{{ emp.name }}</span>
              </div>
            </td>
            <td class="px-4 py-3 text-sm text-gray-600">{{ emp.email }}</td>
            <td class="px-4 py-3 text-sm text-gray-900">
              <span v-html="emp.role"></span>
            </td>
            <td class="px-4 py-3">
              <span class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-gray-100 text-gray-800">
                {{ emp.department }}
              </span>
            </td>
            <td class="px-4 py-3">
              <span 
                :class="[
                  'inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium',
                  emp.status === 'Full-time' 
                    ? 'bg-green-100 text-green-800' 
                    : 'bg-yellow-100 text-yellow-800'
                ]"
              >
                • {{ emp.status }}
              </span>
            </td>
            <td class="px-4 py-3">
              <div class="flex gap-1">
                <button class="p-1.5 text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded transition-colors">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                  </svg>
                </button>
                <button class="p-1.5 text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded transition-colors">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 5v.01M12 12v.01M12 19v.01M12 6a1 1 0 110-2 1 1 0 010 2zM12 13a1 1 0 110-2 1 1 0 010 2zM12 20a1 1 0 110-2 1 1 0 010 2z" />
                  </svg>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
const employees = [
  {
    id: 'TUR87129',
    name: 'Vollny Coelho',
    email: 'vollnycoelho@gmail.com',
    avatar: 'https://i.pravatar.cc/30?img=1',
    role: '<strong>Sr</strong> UIUX Designer',
    department: 'Team Projects',
    status: 'Full-time'
  },
  {
    id: 'TUR85103',
    name: 'Tanish Hramalkar',
    email: 'tanish@gmail.com',
    avatar: 'https://i.pravatar.cc/30?img=2',
    role: '<strong>Lead</strong> Product Designer',
    department: 'Head of Projects',
    status: 'Full-time'
  },
  {
    id: 'TUR715481',
    name: 'Keyes Ahmed',
    email: 'keyes.tur@mail.com',
    avatar: 'https://i.pravatar.cc/30?img=3',
    role: '<strong>Sr</strong> UX Designer',
    department: 'Client & Team Work',
    status: 'Full-time'
  },
  {
    id: 'TUR016481',
    name: 'Turja Sen Das',
    email: 'turja.tur@mail.com',
    avatar: 'https://i.pravatar.cc/30?img=4',
    role: '<strong>Mid</strong> UI Designer',
    department: 'Case Study',
    status: 'Freelance'
  }
]
</script>