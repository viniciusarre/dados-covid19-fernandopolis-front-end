<script>
import { Line } from 'vue-chartjs'
export default {
  mixins: [Line],
  data () {
    return {
      chartData: []
    }
  },
  mounted () {
    this.$papa.parse(
      'https://raw.githubusercontent.com/ShironCat/covid19-fernandopolis-dec2021-data/main/data.csv',
      { header: true, download: true, complete: _ => this.setChartData(_) }
    )
  },
  methods: {
    setChartData (result) {
      const { data } = result
      const labels = data.map(d => d.Data)
      const total = data.map(d => (parseInt(d.Positivos)))

      this.chartData = {
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
      this.renderChart(this.chartData, options)
    }
  }
}
</script>
