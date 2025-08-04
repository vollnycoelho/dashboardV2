<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-6">
      <h3 class="text-lg font-semibold text-gray-900">Employee Performance Ratings</h3>
      <MoreHorizontal class="w-5 h-5 text-gray-400 cursor-pointer" />
    </div>
    
    <div class="mb-6">
      <div class="flex items-baseline space-x-2 mb-2">
        <span class="text-4xl font-bold text-gray-900">98%</span>
      </div>
      <p class="text-sm text-gray-600 leading-relaxed">At Tur Agency, we're proud of our employees' consistent punctuality and quality work</p>
    </div>

    <!-- Performance Chart -->
    <div ref="chartDiv" class="h-64 w-full mb-6"></div>

    <!-- Legend -->
    <div class="flex items-center justify-start space-x-8 text-sm">
      <div class="flex items-center">
        <div class="w-3 h-3 bg-purple-500 rounded-full mr-2"></div>
        <span class="text-gray-700">Task completed</span>
      </div>
      <div class="flex items-center">
        <div class="w-3 h-3 bg-blue-400 rounded-full mr-2"></div>
        <span class="text-gray-700">Presence</span>
      </div>
      <div class="flex items-center">
        <div class="w-3 h-3 bg-teal-400 rounded-full mr-2"></div>
        <span class="text-gray-700">Completed Meeting</span>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref, onUnmounted } from 'vue'
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
    let root = null

    onMounted(() => {
      // Create root
      root = am5.Root.new(chartDiv.value)
      root.setThemes([am5themes_Animated.new(root)])

      // Create chart
      let chart = root.container.children.push(
        am5xy.XYChart.new(root, {
          panX: false,
          panY: false,
          wheelX: "none",
          wheelY: "none",
          layout: root.verticalLayout
        })
      )

      // Data - matching the image
      let data = [
        { name: "Ahsan Tapadar", task: 12, presence: 8, meeting: 10 },
        { name: "Koyes Ahmed", task: 14, presence: 6, meeting: 12 },
        { name: "Washi Bin M.", task: 16, presence: 7, meeting: 9 },
        { name: "Mir Muhain", task: 10, presence: 9, meeting: 8 },
        { name: "Turja Sen Das", task: 18, presence: 5, meeting: 12 }
      ]

      // Create Y-axis (categories)
      let yAxis = chart.yAxes.push(
        am5xy.CategoryAxis.new(root, {
          categoryField: "name",
          renderer: am5xy.AxisRendererY.new(root, {
            inversed: true,
            cellStartLocation: 0.1,
            cellEndLocation: 0.9,
            minGridDistance: 20
          })
        })
      )

      yAxis.get("renderer").labels.template.setAll({
        fontSize: 12,
        fontWeight: "400",
        fill: am5.color("#374151")
      })

      yAxis.get("renderer").grid.template.setAll({
        strokeOpacity: 0
      })

      yAxis.data.setAll(data)

      // Create X-axis (values)
      let xAxis = chart.xAxes.push(
        am5xy.ValueAxis.new(root, {
          renderer: am5xy.AxisRendererX.new(root, {
            minGridDistance: 40
          }),
          min: 0,
          max: 40
        })
      )

      xAxis.get("renderer").labels.template.setAll({
        fontSize: 11,
        fill: am5.color("#9CA3AF")
      })

      xAxis.get("renderer").grid.template.setAll({
        strokeDasharray: [1, 3],
        strokeOpacity: 0.3
      })

      // Create series function
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
          strokeWidth: 0,
          cornerRadiusBR: 4,
          cornerRadiusTR: 4,
          cornerRadiusBL: 4,
          cornerRadiusTL: 4,
          height: am5.percent(60)
        })

        series.data.setAll(data)
        return series
      }

      // Create the three series with matching colors
      createSeries("Task completed", "task", "#8B5CF6") // Purple
      createSeries("Presence", "presence", "#60A5FA")   // Blue
      createSeries("Completed Meeting", "meeting", "#4ADE80") // Teal/Green

      // Hide chart cursor
      chart.set("cursor", am5xy.XYCursor.new(root, {
        behavior: "none"
      }))
    })

    onUnmounted(() => {
      if (root) {
        root.dispose()
      }
    })

    return {
      chartDiv
    }
  }
}
</script>