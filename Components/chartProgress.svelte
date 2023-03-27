<script>
  import { Chart } from "chart.js/auto";
  import { onMount } from "svelte";

  let chartConnect;
  export let percent;

  onMount(() => {
    const progressBar = {
      id: "progressBar",
      beforeDatasetsDraw(chart) {
        const {
          ctx,
          data,
          chartArea: { top, bottom, left, right, width, height },
          scales: { x, y },
        } = chart;

        ctx.save();
        const barHeight =
          (height / y.ticks.length) *
          data.datasets[0].barPercentage *
          data.datasets[0].categoryPercentage;

        data.datasets[0].data.forEach((datapoint, index) => {
          // texto do nome da barra
          const fontSizeLabel = 18;
          ctx.font = `${fontSizeLabel}px sans-serif`;
          ctx.fillStyle = "rgba(0, 0, 0, 1)";
          ctx.textAlign = "left";
          ctx.textBaseline = "middle";
          ctx.fillText(
            data.labels[index],
            left,
            y.getPixelForValue(index) - fontSizeLabel - 5
          );

          //texto de Valor
          const fontSizeDatapoint = 18;
          ctx.font = `${fontSizeDatapoint}px sans-serif`;
          ctx.fillStyle = "rgba(0, 0, 0, 1)";
          ctx.textAlign = "right";
          ctx.textBaseline = "middle";
          ctx.fillText(
            datapoint + "%",
            right,
            y.getPixelForValue(index) - fontSizeDatapoint - 5
          );

          //background color progressbar
          ctx.beginPath();
          ctx.fillStyle = data.datasets[0].borderColor[index];
          ctx.fillRect(
            left,
            y.getPixelForValue(index) - barHeight / 2,
            width,
            barHeight
          );
        });
      },
    };

    const stackedBar = new Chart(chartConnect, {
      type: "bar",
      data: {
        labels: ["Dispobilidade total do turno."],
        datasets: [
          {
            data: [percent, 100],
            backgroundColor: ["#E73536"],
            borderWidth: 0,
            borderColor: ["#D9D9D9"],
            barPercentage: 0.2,
            categoryPercentage: 0.5,
          },
        ],
      },
      options: {
        indexAxis: "y",
        plugins: {
          legend: {
            display: false,
          },
        },
        scales: {
          x: {
            display: false,
            border: {
              display: false,
            },
            ticks: {
              font: {
                size: 20, // tamanho da fonte em pixels
              },
            },
          },
          y: {
            suggestedMax: 100,
            display: false,
            beginAtZero: true,
            border: {
              display: false,
            },
            ticks: {
              display: false,
            },
          },
        },
      },
      plugins: [progressBar],
    });
  });
</script>

<canvas bind:this={chartConnect} />

<!-- Basta importar este componete na sua página principal do código e modificar a o width do chart no style da página principal  -->

<style>
</style>
