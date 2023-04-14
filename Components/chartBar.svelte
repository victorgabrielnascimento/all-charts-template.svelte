<script>
  import { onMount } from "svelte";
  import { Chart } from "chart.js";
  import ChartDataLabels from "chartjs-plugin-datalabels";

  let chartOEE;

  onMount(() => {
    const stackedBar = new Chart(chartOEE, {
      type: "bar",
      data: {
        labels: ["Total", "Atual"],
        datasets: [
          {
            label: "Disponibilidade",
            data: [90, 95],
            backgroundColor: ["#09AE87", "#DB3233"],
            borderWidth: 1,
            barPercentage: 0.6,
          },
        ],
      },
      options: {
        maintainAspectRatio: false,
        scales: {
          x: {
            grid: {
              color: "#C6C6C6",
              display: false,
            },
            ticks: {
              font: {
                size: 14,
                family: "Gotham",
              },
              color: "black",
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
              color: "black",
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
          datalabels: {
            color: "Black",
            anchor: "end",
            align: "start",
            font: {
              size: 16,
              family: "Gotham",
            },
            formatter: function (value, context) {
              return value + "%";
            },
          },
        },
      },
      plugins: [ChartDataLabels],
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
