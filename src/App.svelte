<script lang="ts">
  import Line from "svelte-chartjs/src/Line.svelte";

  const options = {
    scales: {
      BTC: {
        beginAtZero: true,
        position: "right",
        title: {
          display: true,
          text: "BTC",
        },
        ticks: {
          userCallback: function (value, index, values) {
            return value.toLocaleString();
          },
        },
      },
      ETH: {
        beginAtZero: true,
        position: "right",
        title: {
          display: true,
          text: "ETH",
        },
        ticks: {
          userCallback: function (value, index, values) {
            return value.toLocaleString();
          },
        },
      },
      XRP: {
        beginAtZero: true,
        position: "right",
        title: {
          display: true,
          text: "XRP",
        },
        ticks: {
          userCallback: function (value, index, values) {
            return value.toLocaleString();
          },
        },
      },
      ADA: {
        beginAtZero: true,
        position: "right",
        title: {
          display: true,
          text: "ADA",
        },
        ticks: {
          userCallback: function (value, index, values) {
            return value.toLocaleString();
          },
        },
      },
      EOS: {
        beginAtZero: true,
        position: "right",
        title: {
          display: true,
          text: "EOS",
        },
        ticks: {
          userCallback: function (value, index, values) {
            return value.toLocaleString();
          },
        },
      },
    },
    plugins: {
      legend: {
        display: true,
        position: "bottom",
      },
    },
  };

  const data = {
    labels: [],
    datasets: [
      {
        label: "BTC",
        yAxisID: "BTC",
        fill: false,
        lineTension: 0.1,
        borderColor: "#000",
        pointRadius: 0,
        data: [],
      },
      {
        label: "ETH",
        yAxisID: "ETH",
        fill: false,
        lineTension: 0.1,
        borderColor: "#f00",
        pointRadius: 0,
        data: [],
      },
      {
        label: "XRP",
        yAxisID: "XRP",
        fill: false,
        lineTension: 0.1,
        borderColor: "#0f0",
        pointRadius: 0,
        data: [],
      },
      {
        label: "ADA",
        yAxisID: "ADA",
        fill: false,
        lineTension: 0.1,
        borderColor: "#00f",
        pointRadius: 0,
        data: [],
      },
      {
        label: "EOS",
        yAxisID: "EOS",
        fill: false,
        lineTension: 0.1,
        borderColor: "#888",
        pointRadius: 0,
        data: [],
      },
    ],
  };

  function load(fsym, index) {
    const url = `https://min-api.cryptocompare.com/data/v2/histoday?fsym=${fsym}&tsym=USD&limit=1000`;
    console.log(url);
    fetch(url)
      .then((r) => r.json())
      .then((d) => {
        console.log(d.Data.Data);
        const labels = [];
        const values = [];
        for (const x of d.Data.Data) {
          labels.push(new Date(1000 * x.time).toISOString().substring(0, 10));
          values.push(x.close);
        }
        data.labels = labels;
        data.datasets[index].data = values;
      })
      .catch((e) => {
        console.log(e);
      });
  }

  load("BTC", 0);
  load("ETH", 1);
  load("XRP", 2);
  load("ADA", 3);
  load("EOS", 4);
</script>

<main>
  <Line {options} {data} />
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
