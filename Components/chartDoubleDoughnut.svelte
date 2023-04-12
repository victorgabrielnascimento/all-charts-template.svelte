<script>
  import { Chart } from "chart.js/auto";
  import { onMount } from "svelte";

  import "chartjs-plugin-datalabels";

  let producao = 45;
  let meta = 75;
  let producaoLabel = `${producao}%`;
  let pieAtual;

  onMount(() => {
    const stackedBar = new Chart(pieAtual, {
      type: "doughnut",
      data: {
        labels: ["OEE"],
        datasets: [
          {
            label: "Meta Estabelecida",
            data: [meta, 100 - meta],
            backgroundColor: ["#09AE87", "#D9D9D9"],
            borderWidth: 1,
            cutout: 100,
            categoryPercentage: 5,
          },
          {
            label: "OEE Atual",
            data: [producao, 100 - producao],
            backgroundColor: ["#09AE87", "#D9D9D9"],
            borderWidth: 1,
            cutout: 90,
          },
        ],
      },
      options: {
        scales: {
          y: {
            beginAtZero: true,
            display: false,
          },
        },
        plugins: {
          legend: {
            labels: {
              boxWidth: 0,
              color: "black",
              font: {
                size: 13, // tamanho da fonte em pixels
                family: "Montserrat, sans-serif",
                weight: "bolder",
              },
            },
          },
          datalabels: {
            formatter: (value, ctx) => {
              return "${value}%";
            },
            color: "#000000",
            font: {
              weight: "bold",
              size: 200,
            },
          },
        },
      },
    });
  });
</script>

<div class="canvas">
  <canvas bind:this={pieAtual} />
</div>
<h3>{producaoLabel}</h3>

<style>
  .canvas {
    height: 300px;
    width: 100%;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  h3 {
    font-size: 280%;
    font-family: "Montserrat", sans-serif;
    font-weight: bolder;
    text-align: center;
    margin-top: -170px;
    pointer-events: none;
  }
  @media screen and (max-width: 700px) {
    .canvas {
      height: 300px;
      width: 100%;
      text-align: center;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    h3 {
      font-size: 120%;
      font-family: "Montserrat", sans-serif;
      font-weight: bolder;
      text-align: center;
      margin-top: -70px;
      pointer-events: none;
    }
  }
</style>
