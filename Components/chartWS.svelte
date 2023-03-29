<!-- Chart Working and Stop -->
<script>
  import { onMount } from "svelte";
  import { Chart } from "chart.js";
  import "chartjs-adapter-luxon";

  export let stoppedTime = [];
  export let workingTime = [];

  let chartSWPD;

  onMount(() => {
    const data = {
      labels: ["Status"],
      datasets: [
        {
          label: "Parado",
          data: [50],
          backgroundColor: "red",
          barPercentage: 1.0,
          categoryPercentage: 1.0,
        },
        {
          label: "Operando",
          data: [30],
          backgroundColor: "green",
          barPercentage: 1.0,
          categoryPercentage: 1.0,
        },
      ],
    };

    // config
    const config = {
      type: "bar",
      data,
      options: {
        maintainAspectRatio: false,
        indexAxis: "y",
        plugins: {
          legend: {
            labels: {
              color: "black",
              font: {
                size: 20, // tamanho da fonte em pixels
              },
            },
          },
        },

        scales: {
          x: {
            grid: {
              color: "#C6C6C6",
            },
            ticks: {
              font: {
                size: 16, // tamanho da fonte em pixels
              },
              color: "black",
              stepSize: 1,
            },
          },
          y: {
            stacked: true,
            grid: {
              color: "#C6C6C6",
            },
            ticks: {
              font: {
                size: 20, // tamanho da fonte em pixels
              },
              color: "black",
              min: 1,
              max: 24,
            },
          },
        },
      },
    };

    const stackedBar = new Chart(chartSWPD, Object(config));
  });
</script>

<div class="linhas-working-day">
  <canvas bind:this={chartSWPD} />
</div>

<style>
  .linhas-working-day {
    min-width: 95%;
    height: 250px;
  }
  .linhas-working-day canvas {
    min-width: 100%;
  }
</style>
