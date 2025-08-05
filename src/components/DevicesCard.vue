<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-6">
      <h3 class="text-sm font-medium text-gray-600">Today Used Devices</h3>
      <MoreHorizontal class="w-4 h-4 text-gray-400" />
    </div>
    
    <div class="flex items-center space-x-6">
      <!-- amCharts Circular Progress -->
      <div class="relative">
        <div :id="chartId" class="w-28 h-28"></div>
        <div class="absolute inset-0 flex items-center justify-center">
          <div class="text-center">
            <div class="text-xl font-bold text-gray-900">{{ totalDevices }}</div>
            <div class="text-sm text-gray-500">Overall</div>
          </div>
        </div>
      </div>

      <!-- Device Stats -->
      <div class="flex-1 space-y-2">
        <div 
          v-for="device in devices" 
          :key="device.name"
          class="flex items-center justify-between"
        >
          <div class="flex items-center">
            <div 
              class="w-2 h-2 rounded-full mr-2" 
              :style="{ backgroundColor: device.color }"
            ></div>
            <span class="text-sm text-gray-600">{{ device.name }}</span>
          </div>
          <span class="text-sm font-semibold text-gray-900">{{ device.value.toString().padStart(2, '0') }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { MoreHorizontal } from 'lucide-vue-next'
import * as am5 from "@amcharts/amcharts5"
import * as am5percent from "@amcharts/amcharts5/percent"
import am5themes_Animated from "@amcharts/amcharts5/themes/Animated"

export default {
  name: 'DevicesCard',
  components: {
    MoreHorizontal
  },
  props: {
    devices: {
      type: Array,
      default: () => [
        { name: 'Macbook', value: 80, color: '#8b5cf6' },
        { name: 'Keyboard', value: 13, color: '#fb923c' },
        { name: 'Headphones', value: 7, color: '#d1d5db' }
      ]
    }
  },
  data() {
    return {
      chartId: `devices-chart-${Math.random().toString(36).substr(2, 9)}`,
      chart: null
    }
  },
  computed: {
    totalDevices() {
      return this.devices.reduce((sum, device) => sum + device.value, 0)
    },
    chartData() {
      return this.devices.map(device => ({
        category: device.name,
        value: device.value,
        color: device.color
      }))
    }
  },
  mounted() {
    this.createChart()
  },
  beforeUnmount() {
    this.disposeChart()
  },
  methods: {
    createChart() {
      // Create root element
      let root = am5.Root.new(this.chartId)
      
      // Set themes
      root.setThemes([am5themes_Animated.new(root)])
      
      // Create chart - semicircle configuration with proper positioning
      let chart = root.container.children.push(am5percent.PieChart.new(root, {
        startAngle: 180,
        endAngle: 360,
        layout: root.verticalLayout,
        innerRadius: am5.percent(50), // Increased from 65% to make ring thicker
        radius: am5.percent(90),
        y: am5.percent(-10) // Move chart up to center the semicircle
      }))
      
      // Create background track first (gray semicircle)
      let backgroundSeries = chart.series.push(am5percent.PieSeries.new(root, {
        valueField: "value",
        categoryField: "category", 
        startAngle: 180,
        endAngle: 360,
        innerRadius: am5.percent(50),
        radius: am5.percent(90)
      }))
      
      backgroundSeries.slices.template.setAll({
        fill: am5.color("#f1f5f9"),
        stroke: am5.color("#ffffff"),
        strokeWidth: 2,
        cornerRadius: 6
      })
      
      backgroundSeries.labels.template.set("visible", false)
      backgroundSeries.ticks.template.set("visible", false)
      
      // Set background data (full semicircle)
      backgroundSeries.data.setAll([
        { category: "background", value: 100 }
      ])
      
      // Create main data series
      let series = chart.series.push(am5percent.PieSeries.new(root, {
        valueField: "value",
        categoryField: "category",
        startAngle: 180,
        endAngle: 360,
        innerRadius: am5.percent(50),
        radius: am5.percent(90)
      }))
      
      // Remove labels and ticks
      series.labels.template.set("visible", false)
      series.ticks.template.set("visible", false)
      
      // Set slice properties for rounded ends and thicker ring
      series.slices.template.setAll({
        cornerRadius: 6,
        stroke: am5.color("#ffffff"),
        strokeWidth: 2
      })
      
      // Configure colors to match each device
      series.slices.template.adapters.add("fill", (fill, target) => {
        const dataItem = target.dataItem
        if (dataItem) {
          const color = dataItem.dataContext.color
          return am5.color(color)
        }
        return fill
      })
      
      // Set actual data
      series.data.setAll(this.chartData)
      
      // Animate on load
      backgroundSeries.appear(800, 100)
      series.appear(1000, 100)
      
      this.chart = root
    },
    
    disposeChart() {
      if (this.chart) {
        this.chart.dispose()
      }
    }
  },
  watch: {
    devices: {
      handler() {
        if (this.chart) {
          this.disposeChart()
          this.$nextTick(() => {
            this.createChart()
          })
        }
      },
      deep: true
    }
  }
}
</script>

<style scoped>
/* Ensure proper chart container sizing and positioning */
[id*="devices-chart"] {
  width: 112px !important;
  height: 112px !important;
}

/* Center the chart content */
[id*="devices-chart"] .am5-container {
  overflow: visible;
}
</style>