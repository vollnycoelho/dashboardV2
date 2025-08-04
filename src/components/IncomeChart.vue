<template>
  <div class="bg-white rounded-xl shadow-sm border border-gray-400 p-6">
    <div class="flex items-center justify-between mb-4">
      <h3 class="text-lg font-semibold text-gray-800">Income Statistics</h3>
      <div class="flex items-center space-x-2">
        <span class="text-sm text-gray-500">Advance Filter</span>
        <ChevronRight class="w-4 h-4 text-gray-400" />
      </div>
    </div>

    <div class="mb-4 space-y-2">
      <div class="flex items-center justify-between">
        <div class="flex items-center">
          <div class="w-3 h-3 bg-purple-500 rounded-full mr-2"></div>
          <span class="text-sm text-gray-600">Income</span>
        </div>
        <span class="text-sm font-semibold text-gray-900">$2198.11</span>
      </div>
      <div class="flex items-center justify-between">
        <div class="flex items-center">
          <div class="w-3 h-3 bg-blue-400 rounded-full mr-2"></div>
          <span class="text-sm text-gray-600">Expense</span>
        </div>
        <span class="text-sm font-semibold text-gray-900">$733.43</span>
      </div>
    </div>

    <div ref="chartDiv" class="h-64 w-full"></div>
  </div>
</template>

<script>
import { onMounted, ref, onBeforeUnmount } from 'vue' // Import onBeforeUnmount for proper cleanup
import { ChevronRight } from 'lucide-vue-next'
import * as am5 from "@amcharts/amcharts5"
import * as am5xy from "@amcharts/amcharts5/xy"
import am5themes_Animated from "@amcharts/amcharts5/themes/Animated"

export default {
  name: 'IncomeChart',
  components: {
    ChevronRight
  },
  setup() {
    const chartDiv = ref(null)
    let root = null; // Declare root outside onMounted to make it accessible for cleanup

    onMounted(() => {
      // Create root
      root = am5.Root.new(chartDiv.value); // Assign to root variable
      root.setThemes([am5themes_Animated.new(root)]);

      // Set locale for number formatting (comma as decimal separator)
      // This is crucial for matching "$2198,11" format
      root.numberFormatter.set("numberFormat", "#,###.#");
      root.numberFormatter.set("decimalSeparator", ",");
      root.numberFormatter.set("thousandsSeparator", ".");

      // Create chart
      let chart = root.container.children.push(
        am5xy.XYChart.new(root, {
          // No pan/zoom to keep it static like the image
        })
      );

      // Data - Adjusted to visually match the image as closely as possible
      let data = [
        { month: "Jan", income: 3000, expense: 1000 },
        { month: "Feb", income: 3800, expense: 1200 },
        { month: "Mar", income: 6000, expense: 2000 },
        { month: "Apr", income: 7500, expense: 2500 },
        { month: "May", income: 2198.11, expense: 733.43 }, // Exact values from image tooltip
        { month: "Jun", income: 5500, expense: 1800 },
        { month: "Jul", income: 4500, expense: 1500 },
        { month: "Aug", income: 5800, expense: 1900 },
        { month: "Sep", income: 8500, expense: 2800 },
        { month: "Oct", income: 7000, expense: 2300 },
        { month: "Nov", income: 5000, expense: 1600 },
        { month: "Dec", income: 4000, expense: 1300 }
      ];

      // Create axes
      let xAxis = chart.xAxes.push(
        am5xy.CategoryAxis.new(root, {
          categoryField: "month",
          renderer: am5xy.AxisRendererX.new(root, {
            // Remove grid lines for x-axis as per image
            minorGridEnabled: false,
            // Adjust cell locations to make columns wider and closer
            cellStartLocation: 0.2,
            cellEndLocation: 0.8
          }),
          // Labels below the axis
          // labels.template.setAll({
          //   paddingTop: 10
          // })
        })
      );
      xAxis.data.setAll(data);

      let yAxis = chart.yAxes.push(
        am5xy.ValueAxis.new(root, {
          renderer: am5xy.AxisRendererY.new(root, {
            min: 0,
            max: 13000, // Matches image max Y value
            step: 3000, // Matches 3k intervals (0, 3k, 6k, 9k, 12k)
            numberFormat: "$#,###k", // Format as $Xk for axis labels
            minGridDistance: 30 // Ensure grid lines are not too dense
          }),
          // Labels on the left, add padding for spacing
          // labels.template.setAll({
          //   paddingRight: 10
          // })
        })
      );

      // Custom formatting for Y-axis labels to show $0, $3k, etc.
      yAxis.get("renderer").labels.template.adapters.add("text", function(text, target) {
        if (target.dataItem) {
          let value = target.dataItem.get("value");
          if (value === 0) {
            return "$0";
          }
          return "$" + (value / 1000) + "k";
        }
        return text;
      });

      // Create series
      function createSeries(name, field, color, isPatterned) {
        let series = chart.series.push(
          am5xy.ColumnSeries.new(root, {
            name: name,
            xAxis: xAxis,
            yAxis: yAxis,
            valueYField: field,
            categoryXField: "month",
            stacked: true, // For stacked columns
            tooltip: am5.Tooltip.new(root, {
              labelText: "{name}: ${valueY}" // Tooltip format "$VALUE"
            })
          })
        );

        series.columns.template.setAll({
          cornerRadiusTL: 4, // Rounded top corners
          cornerRadiusTR: 4,
          fill: am5.color(color),
          stroke: am5.color(color), // Same color for stroke
          strokeWidth: 0 // No visible stroke line
        });

        if (isPatterned) {
          // Create a pattern for the expense bars
          let pattern = am5.LinePattern.new(root, {
            // The pattern itself will be the fill, so fill color is not needed here
            strokeWidth: 2, // Thickness of the stripes
            stroke: am5.color("#FFFFFF"), // White stripes
            rotation: 45, // Diagonal stripes
            gap: 6, // Distance between stripes
          });

          // Set the pattern as the fill
          series.columns.template.set("fillPattern", pattern);
          // To ensure the base color shows through the pattern, set it here too
          series.columns.template.set("fill", am5.color(color));

        }

        series.data.setAll(data);
        return series;
      }

      // Order matters for stacking: Expense first (bottom), then Income (top)
      createSeries("Expense", "expense", "#3B82F6", true); // Blue with pattern
      createSeries("Income", "income", "#8B5CF6", false); // Purple without pattern

      // Add cursor for interactive tooltips on hover
      let cursor = chart.set("cursor", am5xy.XYCursor.new(root, {
        behavior: "none" // No panning/zooming with cursor
      }));
      cursor.lineX.set("visible", false); // Hide vertical line
      cursor.lineY.set("visible", false); // Hide horizontal line

      // Tooltip background and border style to match image (white background, shadow)
      chart.get("tooltip").get("background").setAll({
        fill: am5.color(0xFFFFFF),
        fillOpacity: 1,
        stroke: am5.color(0x000000),
        strokeOpacity: 0.1,
        strokeWidth: 1,
        cornerRadius: 6,
        shadowColor: am5.color(0x000000),
        shadowBlur: 10,
        shadowOffsetX: 2,
        shadowOffsetY: 2,
        shadowOpacity: 0.1
      });

      // Tooltip label styling
      chart.get("tooltip").label.setAll({
        fill: am5.color(0x000000) // Black text for tooltip
      });
    });

    // Cleanup function when component unmounts
    onBeforeUnmount(() => {
      if (root) {
        root.dispose();
      }
    });

    return {
      chartDiv
    };
  }
};
</script>

<style scoped>
/* No specific styles needed here, AmCharts handles rendering */
</style>