---
layout: post
title: Price of happiness
---

Last year i took a £25,000 pay cut

<!--kg-card-begin: html--><svg class="line-chart"></svg><script src="https://cdn.jsdelivr.net/npm/chart.xkcd@1.1/dist/chart.xkcd.min.js"></script><script>
  const svg = document.querySelector('.line-chart')

  const lineChart = new chartXkcd.Line(svg, {
    title: 'Subjective happiness compared to salary', // optional
    xLabel: 'Year', // optional
    yLabel: '£ in Thousands', // optional
    data: {
      labels: ['2009', '2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017', '2018', '2019'],
      datasets: [{
        label: 'Salary',
        data: [22000, 24000, 26500, 35000, 35000, 35000, 37500, 45000, 65000, 75000, 53000],
      }, {
        label: 'Happiness',
        data: [30000, 32000, 35000, 35000, 35000, 30000, 40000, 40000, 20000, 16000, 60000],
      }],
    },
    options: { // optional
      yTickCount: 3,
      legendPosition: chartXkcd.config.positionType.upLeft
    }
  });
</script><!--kg-card-end: html-->