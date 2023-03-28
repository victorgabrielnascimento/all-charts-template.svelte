<script>
  import { Chart } from "chart.js/auto";
  import "chartjs-plugin-datalabels";
  import { onMount } from "svelte";

  let chartProducao;
  let producao = 67;
  let producaoLabel = `${producao}%`;

  onMount(() => {
    const doughnutChart = new Chart(chartProducao, {
      type: "doughnut",
      data: {
        labels: [""],
        datasets: [
          {
            label: "Produção",
            data: [producao, 100 - producao],
            backgroundColor: ["#09AE87", "#B2B2B2"],
            circumference: 180,
            rotation: 270,
          },
        ],
      },
      options: {
        plugins: {
          legend: {
            display: false,
          },
          datalabels: {
            display: true,
            formatter: function (value, context) {
              return Math.round(value) + "%";
            },
            color: "red",
            font: {
              size: 30,
              weight: "bold",
            },
          },
        },
        layout: {
          padding: {
            bottom: 30,
          },
        },
        cutout: "60%",
      },
    });
  });

  function textCenter(val) {
    Chart.pluginService.register({
      beforeDraw: function (chart) {
        var width = chart.chart.width,
          height = chart.chart.height,
          ctx = chart.chart.ctx;

        ctx.restore();
        var fontSize = (height / 114).toFixed(2);
        ctx.font = fontSize + "em sans-serif";
        ctx.textBaseline = "middle";

        var text = val + "%",
          textX = Math.round((width - ctx.measureText(text).width) / 2),
          textY = height / 2;

        ctx.fillText(text, textX, textY);
        ctx.save();
      },
    });
  }
</script>

<div class="grafico">
  <canvas bind:this={chartProducao} />
  <h2>OEE</h2>
  <h3>{producaoLabel}</h3>
</div>

<style>
  .grafico {
    width: 80%;
    height: 158%;
    margin-top: -22%;
  }
  .grafico h2 {
    margin-top: -52%;
    font-size: 120%;
    font-family: "Montserrat", sans-serif;
    font-weight: 300;
    text-align: center;
  }
  .grafico h3 {
    font-size: 200%;
    font-family: "Montserrat", sans-serif;
    font-weight: bolder;
    text-align: center;
  }
  @media screen and (max-width: 700px) {
    .grafico {
      justify-content: center;
    }
    .grafico h2 {
      margin-top: -54%;
      font-size: 110%;
      font-family: "Montserrat", sans-serif;
      font-weight: 300;
      text-align: center;
    }
    .grafico h3 {
      font-size: 180%;
      font-family: "Montserrat", sans-serif;
      font-weight: bolder;
      text-align: center;
    }
  }
</style>
