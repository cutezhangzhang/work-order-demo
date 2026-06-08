<template>
  <div
    ref="chartRef"
    style="width: 100%; height: 400px; margin-top: 40px"
  ></div>
</template>

<script setup>
import * as echarts from 'echarts'
import { onMounted, ref, watch } from 'vue'

const props = defineProps({
  tableData: Array
})

const chartRef = ref(null)

let myChart = null

const renderChart = () => {

  const projectMap = {}

  props.tableData.forEach(item => {

    if (!projectMap[item.project]) {
      projectMap[item.project] = 0
    }

    projectMap[item.project] += item.hours
  })

  const option = {
    title: {
      text: 'Project Hours Distribution'
    },

    tooltip: {},

    xAxis: {
      type: 'category',
      data: Object.keys(projectMap)
    },

    yAxis: {
      type: 'value'
    },

    series: [
      {
        type: 'bar',
        data: Object.values(projectMap)
      }
    ]
  }

  myChart.setOption(option)
}

onMounted(() => {

  myChart = echarts.init(chartRef.value)

  renderChart()
})

watch(
  () => props.tableData,
  () => {
    renderChart()
  },
  {
    deep: true
  }
)
</script>