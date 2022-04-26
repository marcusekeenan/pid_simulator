<template>
<div>
  <apexchart width="100%" height="600px" type="line" :options="chartOptions" :series="seriesData"></apexchart>
   {{ PID001 }}
</div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
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
  data () {
    return {
      chartOptions: {
        chart: {
          id: 'realtime',
          height: 350,
          type: 'line',
          animations: {
            enabled: true,
            easing: 'linear',
            dynamicAnimation: {
              speed: 1000
            }
          },
          toolbar: {
            show: false
          },
          legend: {
            show: true
          },
          zoom: {
            enabled: false
          }
        },
        dataLabels: {
          enabled: false
        },
        title: {
          text: 'Dynamic Updating Chart',
          align: 'left'
        },
        markers: {
          size: 0
        },
        xaxis: {
          type: 'datetime',
          range: 100000,
          labels: {
            style: {
              colors: '#FFFFFF',
              fontSize: '12px',
              fontFamily: 'Helvetica, Arial, sans-serif',
              fontWeight: 400,
              cssClass: 'apexcharts-xaxis-label'
            }
          }
        },
        yaxis: [
          {
            max: () => 300.0,
            labels: {
              style: {
                colors: '#FFFFFF'
              },
              formatter: function (val) {
                return val.toFixed(2)
              }
            },
            title: {
              text: 'PV',
              style: {
                color: '#FFFFFF'
              }
            }
          },
          {
            opposite: true,
            max: () => 300.0,
            labels: {
              style: {
                colors: '#FFFFFF'
              },
              formatter: function (val) {
                return val.toFixed(2)
              }
            },
            title: {
              text: 'SP',
              style: {
                color: '#FFFFFF'
              }
            }
          },
          {
            opposite: true,
            max: 110.0,
            labels: {
              style: {
                colors: '#FFFFFF'
              },
              formatter: function (val) {
                return val.toFixed(2)
              }
            },
            title: {
              text: 'CV',
              style: {
                color: '#FFFFFF'
              }
            }
          }
        ],
        legend: {
          show: true,
          labels: {
            colors: '#FFFFFF',
            useSeriesColors: false
          }
        },
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
        stroke: {
          show: true,
          curve: 'smooth',
          lineCap: 'butt',
          colors: undefined,
          width: 4,
          dashArray: 0
        }
      }

    }
  }
  // updated () {
  //   //const me = this
  //   window.setInterval(function () {
  //     // eslint-disable-next-line

  //     // me.$refs.chart.updateSeries([{
  //     //   data: this.seriesData.slice()
  //     // }])
  //   }, 1000)
  // }
})
</script>
