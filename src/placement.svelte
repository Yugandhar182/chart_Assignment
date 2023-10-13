<script>
    import { onMount } from 'svelte';
    import { Chart, StackingColumnSeries, Category, DataLabel, Tooltip, Legend,Highlight } from '@syncfusion/ej2-charts';
    import { Browser } from '@syncfusion/ej2-base';

    Chart.Inject(StackingColumnSeries, Category, DataLabel, Tooltip, Legend,Highlight);

    let chartData = []; // Initialize with an empty array

    // Define an array of month names
    const monthNames = [
        '2023 January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
    ];

    onMount(async () => {
        // Fetch data from the API
        const apiUrl = 'https://api.recruitly.io/api/dashboard/ats/data/placementmonthlyusermetrics?start=01%2F01%2F2023&end=11%2F10%2F2023&apiKey=TEST45684CB2A93F41FC40869DC739BD4D126D77';

        try {
            const response = await fetch(apiUrl);
            if (response.ok) {
                const jsonData = await response.json();

                // Transform API data into the format suitable for the chart
                chartData = jsonData.map(item => ({
                    x: monthNames[parseInt(item.monthLabel.split('/')[0]) - 1], // Convert numeric month to month name
                    'Andy Barnes': item['Andy Barnes'],
                    'Gary Williams': item['Gary Williams'],
                    'Bob Shaw': item['Bob Shaw']
                }));

                // Sort the chart data by month order
                chartData.sort((a, b) => monthNames.indexOf(a.x) - monthNames.indexOf(b.x));

                // Refresh the chart with the updated data
                updateChart();
            } else {
                console.error('Failed to fetch data from the API.');
            }
        } catch (error) {
            console.error('An error occurred while fetching data:', error);
        }
    });

    // Function to create or update the chart
    function updateChart() {
        // Create and append the chart with the updated data source
        const chart = new Chart({
            primaryXAxis: {
                valueType: 'Category',
                majorGridLines: { width: 0 },
            },
            primaryYAxis: {
                edgeLabelPlacement: 'Shift',
                majorTickLines: { width: 0 },
                minorTickLines: { width: 0 },
                lineStyle: { width: 0 },
                title: 'Placement value',
            },
            width: '1390px', // Set the width of the chart
            height: '400px', // Set the height of the chart
            series: [
                {
                    type: 'StackingColumn',
                    dataSource: chartData,
                    xName: 'x',
                    width: 2,
                    yName: 'Bob Shaw',
                    columnSpacing: 0.2,
                    name: 'Bob Shaw',
                    fill: 'DodgerBlue',
                },
                {
                    type: 'StackingColumn',
                    dataSource: chartData,
                    xName: 'x',
                    width: 2,
                    yName: 'Andy Barnes',
                    columnSpacing: 0.2,
                    name: 'Andy Barnes',
                    fill: 'Tomato',
                },
                {
                    type: 'StackingColumn',
                    dataSource: chartData,
                    xName: 'x',
                    width: 2,
                    yName: 'Gary Williams',
                    columnSpacing: 0.2,
                    name: 'Gary Williams',
                    fill: 'MediumSeaGreen',
                },
            ],
            title: 'Placement by user',
            tooltip: {
                enable: true,
                format: 'GDP ${point.y}', // Customize tooltip format
                template:'#Female-Material'
               
              
            },
            legendSettings: { enableHighlight :true },

        });

        chart.appendTo('#container3');
    }
</script>
<div class="container1">
<div id='container3'></div>
</div>
<style>
       .container1{
        background-color:white;
        width: 1400px;
	    height: 420px;
        margin-left:40px;
        margin-top: 80px;
        border: 4px solid rgb(234, 234, 245);
    }
</style>
