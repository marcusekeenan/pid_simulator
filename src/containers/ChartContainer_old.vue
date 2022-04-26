<template>
<div>
  <apexchart width="100%" height="800px" type="line" :options="chartOptions" :series="seriesData"></apexchart>
</div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'ChartContainer',
  props: {
    title: {
      type: String,
      required: true
    },
    seriesData: {
      type: Array,
      default: () => []
    },
    PID001: {}
  },
  data: function () {
    return {
      nothing: 0
    }
  },
  computed: {
    chartOptions () {
      return {
        chart: {
          id: 'vuechart-example'
        },
        xaxis: {
          type: 'datetime',
          labels: {
            style: {
              colors: '#FFFFFF'
            }
          }
        },
        // yaxis: {
        //   decimalsInFloat: 2,
        //   tickAmount: 6,
        //   forceNiceScale: false
        // },
        yaxis: [
          {
            labels: {
              style: {
                colors: '#FFFFFF'
              }
            },
            min: 0,
            max: 100,
            title: {
              text: 'Series A',
              style: {
                color: '#FFFFFF'
              }
            }
          },
          {
            opposite: true,
            labels: {
              style: {
                colors: '#FFFFFF'
              }
            },
            max: PID001.MAX,
            title: {
              text: 'Series B',
              style: {
                color: '#FFFFFF'
              }
            }
          },
          {
            opposite: true,
            labels: {
              style: {
                colors: '#FFFFFF'
              }
            },
            title: {
              text: 'Series C',
              style: {
                color: '#FFFFFF'
              }
            },
            max: 100,
            min: 0
          }
        ],
        tooltip: {
          enabled: true,
          enabledOnSeries: undefined,
          shared: true,
          followCursor: false,
          intersect: false,
          inverseOrder: false,
          custom: undefined,
          fillSeriesColor: false,
          theme: 'dark',
          style: {
            fontSize: '14px',
            fontFamily: undefined
          },
          onDatasetHover: {
            highlightDataSeries: false
          },
          x: {
            show: true,
            format: 'dd MMM',
            formatter: undefined
          },
          y: {
            formatter: undefined,
            title: {
              formatter: (seriesName) => seriesName
            }
          },
          z: {
            formatter: undefined,
            title: 'Size: '
          },
          marker: {
            show: true
          },
          fixed: {
            enabled: false,
            position: 'topRight',
            offsetX: 0,
            offsetY: 0
          }
        },
        legend: {
          show: true
        },
        stroke: {
          show: true,
          curve: 'smooth',
          lineCap: 'butt',
          colors: undefined,
          width: 2,
          dashArray: 0
        }
      }
    }
  }
})
</script>
