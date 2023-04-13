<script>
  import { Chart } from "chart.js/auto";
  import { onMount } from "svelte";

  import "chartjs-plugin-datalabels";

  let turno1 = 95;
  let turno2 = 65;
  let turno3 = 90;
  let pieTurnos;

  onMount(() => {
    const stackedBar = new Chart(pieTurnos, {
      type: "polarArea",
      data: {
        labels: ["1ºTurno", "2ºTurno", "3ºTurno"],
        datasets: [
          {
            label: "Turnos",
            data: [turno1, turno2, turno3],
            backgroundColor: ["#09AE8790", "#E7D53590", "#00B2FF90"],
            borderWidth: 2,
            borderColor: ["#09AE87", "#E7D535", "#00B2FF"],
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
              boxWidth: 12,
              color: "black",
              font: {
                size: 8,
                family: "Gotham",
              },
            },
            position: "bottom",
          },
          datalabels: {
            formatter: (value, ctx) => {
              return "${value}%";
            },
            color: "#000000",
            font: {
              weight: "bolder",
            },
          },
        },
      },
    });
  });
</script>

<div id="chart">
  <canvas bind:this={pieTurnos} />
</div>

<style>
  #chart {
    display: flex;
    width: 350px;
    height: 180px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  @media screen and (min-width: 1920px) {
    #chart {
      width: 450px;
    }
  }
</style>
