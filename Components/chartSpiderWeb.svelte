<script>
  import { onMount } from "svelte";
  import { Chart } from "chart.js";
  import ChartDataLabels from "chartjs-plugin-datalabels";

  let chartOEE;

  onMount(() => {
    const stackedBar = new Chart(chartOEE, {
      type: "radar",
      data: {
        labels: [
          "Refugo",
          "Retrabalho",
          "Dobra invertida",
          "Respingo de Solda",
          "Acabamento",
        ],
        datasets: [
          {
            label: "Não Conformidades",
            data: [50, 50, 50, 50, 50],
            backgroundColor: [
              "#09AE8760",
              "#DB3233",
              "#09AE87",
              "#DB3233",
              "#DB3233",
            ],
            borderColor: ["#09AE8760"],
            borderWidth: 2, //tamanho do contorno do gráfico
          },
        ],
      },
      options: {
        maintainAspectRatio: false,
        scales: {
          x: {
            grid: {
              display: false,
            },
            ticks: {
              display: false,
            },
            border: {
              display: false,
            },
          },
          y: {
            beginAtZero: true,
            grid: {
              display: false,
            },
            ticks: {
              display: false,
            },
            border: {
              display: false,
            },
          },
        },
        plugins: {
          legend: {
            display: true,
            labels: {
              boxWidth: 0,
              color: "black",
              font: {
                size: 12,
                family: "Gotham",
              },
            },
          },
        },
      },
    });
  });
</script>

<div id="linhas-oee">
  <canvas bind:this={chartOEE} />
</div>

<style>
  #linhas-oee {
    min-width: 90%;
    height: 250px;
  }
  #linhas-oee canvas {
    min-width: 100%;
  }
</style>
