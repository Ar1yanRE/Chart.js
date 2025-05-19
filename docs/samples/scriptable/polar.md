const labels = ['PTS', 'REB', 'AST', 'BLK'];

const data = {
  labels: labels,
  datasets: [
    {
      label: 'Cavaliers',
      data: [50, 8, 5, 2],
      backgroundColor: 'rgba(128, 0, 32, 0.3)', // Maroon
      borderColor: 'rgba(128, 0, 32, 1)',
      pointBackgroundColor: 'rgba(128, 0, 32, 1)',
      borderWidth: 2,
      fill: true
    },
    {
      label: 'Magic',
      data: [27, 9, 4, 2],
      backgroundColor: 'rgba(0, 122, 204, 0.3)', // Blue
      borderColor: 'rgba(0, 122, 204, 1)',
      pointBackgroundColor: 'rgba(0, 122, 204, 1)',
      borderWidth: 2,
      fill: true
    }
  ]
};

const topPlayers = {
  Cavaliers: {
    PTS: 'Donovan Mitchell',
    REB: 'Marcus Morris Sr.',
    AST: 'Darius Garland',
    BLK: 'Evan Mobley'
  },
  Magic: {
    PTS: 'Paolo Banchero',
    REB: 'Wendell Carter Jr.',
    AST: 'Jalen Suggs',
    BLK: 'Franz Wagner'
  }
};

const config = {
  type: 'radar',
  data: data,
  options: {
    responsive: true,
    plugins: {
      legend: {
        position: 'top',
      },
      tooltip: {
        callbacks: {
          label: function (context) {
            const team = context.dataset.label;
            const stat = context.label;
            const value = context.raw;
            const player = topPlayers[team][stat];
            return `${team} - ${stat}: ${value} (${player})`;
          }
        }
      }
    },
    scales: {
      r: {
        beginAtZero: true,
        max: 60,
        ticks: {
          stepSize: 10
        }
      }
    }
  }
};

const actions = [
  {
    name: 'Reset to Team Leaders',
    handler(chart) {
      chart.data.datasets[0].data = [50, 8, 5, 2];
      chart.data.datasets[1].data = [27, 9, 4, 2];
      chart.update();
    }
  }
];

// Render chart
new Chart(
  document.getElementById('myChart'),
  config
);
