<script>
  import { Chart } from "chart.js/auto";
  import { onMount } from "svelte";

  let chartConnect;

  onMount(() => {
    const progressLine = {};

    const stackedBar = new Chart(chartConnect, {
      type: "line",
      data: {
        labels: ["Dom", "Seg", "Ter", "Qua", "Qui", "Sex", "Sab"],
        datasets: [
          {
            label: "Estipulado",
            data: [75, 75, 75, 75, 75, 75, 75],
            fill: true,
            backgroundColor: ["#09AE8720"],
            borderColor: ["#09AE87"],
            tension: 0.1,
          },
          {
            label: "Produção",
            data: [0, 80, 78, 90, 82, 89, 70],
            fill: false,
            backgroundColor: ["#00B2FF60"],
            borderColor: ["#00B2FF"],
            tension: 0.1,
          },
          {
            label: "Incoerencia",
            data: [75, 0, 0, 0, 0, 0, 5],
            fill: true,
            backgroundColor: ["#DB323360"],
            borderColor: ["#DB3233"],
            tension: 0.1,
          },
        ],
      },
      options: {
        plugins: {
          legend: {
            display: true,
            position: "bottom",
          },
        },
        scales: {
          x: {
            display: true,
            border: {
              display: true,
            },
            ticks: {
              font: {
                size: 10, // tamanho da fonte em pixels
                family: "Gotham, sans-serif",
              },
            },
          },
          y: {
            suggestedMax: 100,
            display: true,
            beginAtZero: true,
            border: {
              display: false,
            },
            ticks: {
              display: true,
            },
          },
        },
      },
    });
  });
</script>

<canvas bind:this={chartConnect} />

<style>
</style>
