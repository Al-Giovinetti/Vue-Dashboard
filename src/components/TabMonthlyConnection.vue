<template>
    <div class="tab-month-connections">
        <canvas id="month-connections"></canvas>
    </div>
</template>

<script>
import { Chart } from 'chart.js/auto';

export default {
    name:'TabMonthlyConnection',

    props:{
        monthlyConnection:Array
    },

    data(){
        return{
        }
    },

    methods:{
        createGraph(){
            let monthList = [];
            let connectionList = [];
            console.log(this.dataTab)
           
            this.monthlyConnection.forEach((element) => {
                monthList.push(element.month)
                connectionList.push(element.connections)
            });

            const graph = document.getElementById('month-connections')

            const createGraph = new Chart(graph, {
                type:'line',

                data:{
                    labels: monthList,
                    datasets:[{
                        label:'connections',
                        data: connectionList,
                        backgroundColor: 'red',
                        borderColor: 'blue',
                        fill:'start',
                        tension:0.5,
                    }]
                },
                options:{
                    scales:{
                        y:{
                            beginAtZero:true,
                            min: 0,
                            max: 5000,
                        }
                    },
                    plugins:{
                        title:{
                            display:true,
                            text:'Monthly Connections'
                        }
                    },
                    responsive:true,
                    maintainAspectRatio:false,                  
                }     
            })
            
        },
    },

    watch: {
        monthlyConnection: {
            // Richiama la funzione createGraph quando monthlyConnection cambia - si usa per API (xchè asincrone)
            handler: 'createGraph', 
        },
    },   
}
</script>

<style lang="scss" scoped>
.tab-month-connections{
    height: 30vh;
    text-align: center;
    #month-connections{
        margin: auto;
        width: 100%;
        background-color: white;
    }
}
</style>