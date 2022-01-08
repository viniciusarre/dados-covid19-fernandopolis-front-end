<script>
import { Line } from 'vue-chartjs'
export default {
  mixins: [Line],
  data () {
    return {
      chartdata: []
    }
  },
  mounted () {
    this.$papa.parse(
      'https://raw.githubusercontent.com/ShironCat/covid19-fernandopolis-dec2021-data/main/data.csv',
      { header: true, download: true, complete: _ => this.setChartData(_) }
      // { download: true },
      // _ => console.log(_)
    )
    // this.parseFile()
  },
  methods: {
    setChartData (result) {
      const { data } = result
      const labels = data.map(d => d.Data)
      const total = data.map(d => (parseInt(d.Positivos)))

      this.chartdata = {
        labels,
        datasets: [
          {
            label: 'Total de Casos',
            data: total,
            borderWidth: 3
          }

        ]

      }

      const options = {
        responsive: true,
        maintainAspectRatio: false
      }
      // console.log('this.chartData ', chartData)
      this.renderChart(this.chartdata, options)
    }
  }
}
</script>
