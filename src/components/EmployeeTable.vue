<template>
  <div class="bg-white rounded-lg p-4 shadow-sm border border-gray-400">
    <!-- Header Section -->
    <div class="flex justify-between items-center mb-4">
      <h6 class="text-lg font-semibold text-gray-900 mb-0">All Employees</h6>
      <div class="flex gap-2">
        <input 
          v-model="searchTerm"
          class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent" 
          type="text" 
          placeholder="🔍 Search Employee" 
        />
        <select 
          v-model="statusFilter"
          class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent"
        >
          <option>All Status</option>
          <option>Full-time</option>
          <option>Freelance</option>
        </select>
        <select 
          v-model="roleFilter"
          class="px-3 py-2 text-sm border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent"
        >
          <option>All Role</option>
          <option v-for="role in uniqueRoles" :key="role" :value="role">
            {{ role }}
          </option>
        </select>
        <button 
          @click="exportData"
          class="px-3 py-2 text-sm border border-gray-300 text-gray-700 rounded-md hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-purple-500"
        >
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
                v-model="selectAll"
                @change="toggleSelectAll"
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
          <tr v-for="emp in filteredEmployees" :key="emp.id" class="hover:bg-gray-50">
            <td class="px-4 py-3">
              <input 
                type="checkbox" 
                v-model="selectedEmployees"
                :value="emp.id"
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
              <span v-html="formatRole(emp.role)"></span>
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
                <button 
                  @click="viewEmployee(emp)"
                  class="p-1.5 text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded transition-colors"
                  title="View Employee"
                >
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                  </svg>
                </button>
                <button 
                  @click="showOptions(emp)"
                  class="p-1.5 text-gray-400 hover:text-gray-600 hover:bg-gray-100 rounded transition-colors"
                  title="More Options"
                >
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 5v.01M12 12v.01M12 19v.01M12 6a1 1 0 110-2 1 1 0 010 2zM12 13a1 1 0 110-2 1 1 0 010 2zM12 20a1 1 0 110-2 1 1 0 010 2z" />
                  </svg>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
      
      <!-- No results message -->
      <div v-if="filteredEmployees.length === 0" class="text-center py-8">
        <p class="text-gray-500">No employees found matching your criteria.</p>
      </div>
    </div>
    
    <!-- Results count -->
    <div class="mt-4 text-sm text-gray-600">
      Showing {{ filteredEmployees.length }} of {{ employees.length }} employees
      <span v-if="selectedEmployees.length > 0" class="ml-2">
        ({{ selectedEmployees.length }} selected)
      </span>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

// Reactive data
const searchTerm = ref('')
const statusFilter = ref('All Status')
const roleFilter = ref('All Role')
const selectedEmployees = ref([])
const selectAll = ref(false)

// Employee data
const employees = ref([
  {
    id: 'TUR87129',
    name: 'Vollny Coelho',
    email: 'vollnycoelho@gmail.com',
    avatar: 'https://i.pravatar.cc/30?img=1',
    role: 'Sr UIUX Designer',
    department: 'Team Projects',
    status: 'Full-time'
  },
  {
    id: 'TUR85103',
    name: 'Tanish Hramalkar',
    email: 'tanish@gmail.com',
    avatar: 'https://i.pravatar.cc/30?img=2',
    role: 'Lead Product Designer',
    department: 'Head of Projects',
    status: 'Full-time'
  },
  {
    id: 'TUR715481',
    name: 'Keyes Ahmed',
    email: 'keyes.tur@mail.com',
    avatar: 'https://i.pravatar.cc/30?img=3',
    role: 'Sr UX Designer',
    department: 'Client & Team Work',
    status: 'Full-time'
  },
  {
    id: 'TUR016481',
    name: 'Turja Sen Das',
    email: 'turja.tur@mail.com',
    avatar: 'https://i.pravatar.cc/30?img=4',
    role: 'Mid UI Designer',
    department: 'Case Study',
    status: 'Freelance'
  }
])

// Computed properties
const uniqueRoles = computed(() => {
  const roles = employees.value.map(emp => emp.role)
  return [...new Set(roles)]
})

const filteredEmployees = computed(() => {
  return employees.value.filter(emp => {
    // Search filter
    const matchesSearch = searchTerm.value === '' || 
      emp.name.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      emp.email.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      emp.id.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      emp.role.toLowerCase().includes(searchTerm.value.toLowerCase()) ||
      emp.department.toLowerCase().includes(searchTerm.value.toLowerCase())

    // Status filter
    const matchesStatus = statusFilter.value === 'All Status' || 
      emp.status === statusFilter.value

    // Role filter
    const matchesRole = roleFilter.value === 'All Role' || 
      emp.role === roleFilter.value

    return matchesSearch && matchesStatus && matchesRole
  })
})

// Methods
const toggleSelectAll = () => {
  if (selectAll.value) {
    selectedEmployees.value = filteredEmployees.value.map(emp => emp.id)
  } else {
    selectedEmployees.value = []
  }
}

const formatRole = (role) => {
  // Format role to make certain words bold
  return role.replace(/(Sr|Lead|Mid|Junior)/g, '<strong>$1</strong>')
}

const viewEmployee = (emp) => {
  console.log('Viewing employee:', emp)
  // Add your view logic here
  alert(`Viewing ${emp.name}'s profile`)
}

const showOptions = (emp) => {
  console.log('Options for employee:', emp)
  // Add your options logic here
  alert(`Options for ${emp.name}`)
}

const exportData = () => {
  const dataToExport = selectedEmployees.value.length > 0 
    ? employees.value.filter(emp => selectedEmployees.value.includes(emp.id))
    : filteredEmployees.value

  console.log('Exporting data:', dataToExport)
  
  // Simple CSV export
  const csvContent = [
    ['ID', 'Name', 'Email', 'Role', 'Department', 'Status'],
    ...dataToExport.map(emp => [
      emp.id, 
      emp.name, 
      emp.email, 
      emp.role.replace(/<[^>]*>/g, ''), // Remove HTML tags
      emp.department, 
      emp.status
    ])
  ]
  .map(row => row.join(','))
  .join('\n')

  const blob = new Blob([csvContent], { type: 'text/csv' })
  const url = window.URL.createObjectURL(blob)
  const link = document.createElement('a')
  link.href = url
  link.download = 'employees.csv'
  link.click()
  window.URL.revokeObjectURL(url)
}

// Watch for changes in selected employees to update selectAll
watch(selectedEmployees, (newVal) => {
  selectAll.value = newVal.length === filteredEmployees.value.length && newVal.length > 0
}, { deep: true })

// Watch for changes in filtered employees to update selectAll
watch(filteredEmployees, () => {
  selectAll.value = selectedEmployees.value.length === filteredEmployees.value.length && selectedEmployees.value.length > 0
})
</script>

