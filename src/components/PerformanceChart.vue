<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-lg font-semibold text-gray-800">Employee Performance Ratings</h3>
      <MoreHorizontal class="w-4 h-4 text-gray-400" />
    </div>
    
    <div class="mb-4">
      <div class="flex items-center space-x-2">
        <span class="text-3xl font-bold text-gray-900">98%</span>
      </div>
      <p class="text-sm text-gray-500 mt-1">At Tur Agency, we're proud of our employees' consistent punctuality and quality work</p>
    </div>

    <!-- Performance Chart -->
    <div ref="chartDiv" class="h-64 w-full"></div>

    <!-- Legend -->
    <div class="flex justify-between text-xs mt-4">
      <div class="flex items-center">
        <div class="w-2 h-2 bg-purple-500 rounded-full mr-1"></div>
        <span class="text-gray-600">Task completed</span>
      </div>
      <div class="flex items-center">
        <div class="w-2 h-2 bg-blue-400 rounded-full mr-1"></div>
        <span class="text-gray-600">Presence</span>
      </div>
      <div class="flex items-center">
        <div class="w-2 h-2 bg-green-500 rounded-full mr-1"></div>
        <span class="text-gray-600">Completed Meeting</span>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue'
import { MoreHorizontal } from 'lucide-vue-next'
import * as am5 from "@amcharts/amcharts5"
import * as am5xy from "@amcharts/amcharts5/xy"
import am5themes_Animated from "@amcharts/amcharts5/themes/Animated"

export default {
  name: 'PerformanceChart',
  components: {
    MoreHorizontal
  },
  setup() {
    const chartDiv = ref(null)

    onMounted(() => {
      // Create root
      let root = am5.Root.new(chartDiv.value)
      root.setThemes([am5themes_Animated.new(root)])

      // Create chart
      let chart = root.container.children.push(
        am5xy.XYChart.new(root, {
          panX: false,
          panY: false,
          wheelX: "none",
          wheelY: "none"
        })
      )

      // Data
      let data = [
        { name: "Ahsan Tapadar", task: 35, presence: 25, meeting: 30 },
        { name: "Koyes Ahmed", task: 40, presence: 30, meeting: 35 },
        { name: "Washi Bin M.", task: 45, presence: 25, meeting: 30 },
        { name: "Mir Muhain", task: 25, presence: 30, meeting: 25 },
        { name: "Turja Sen Das", task: 40, presence: 20, meeting: 35 }
      ]

      // Create Y-axis
      let yAxis = chart.yAxes.push(
        am5xy.CategoryAxis.new(root, {
          categoryField: "name",
          renderer: am5xy.AxisRendererY.new(root, {
            inversed: true,
            cellStartLocation: 0.1,
            cellEndLocation: 0.9
          })
        })
      )
      yAxis.data.setAll(data)

      // Create X-axis
      let xAxis = chart.xAxes.push(
        am5xy.ValueAxis.new(root, {
          renderer: am5xy.AxisRendererX.new(root, {}),
          min: 0,
          max: 50
        })
      )

      // Create series
      function createSeries(name, field, color) {
        let series = chart.series.push(
          am5xy.ColumnSeries.new(root, {
            name: name,
            xAxis: xAxis,
            yAxis: yAxis,
            valueXField: field,
            categoryYField: "name",
            stacked: true
          })
        )
        series.columns.template.setAll({
          tooltipText: "{name}: {valueX}",
          fill: am5.color(color),
          stroke: am5.color(color),
          cornerRadiusBR: 3,
          cornerRadiusTR: 3,
          cornerRadiusBL: 3,
          cornerRadiusTL: 3
        })
        series.data.setAll(data)
        return series
      }

      createSeries("Task completed", "task", "#8B5CF6")
      createSeries("Presence", "presence", "#3B82F6")
      createSeries("Completed Meeting", "meeting", "#10B981")

      // Cleanup function
      return () => {
        root.dispose()
      }
    })

    return {
      chartDiv
    }
  }
}
</script>