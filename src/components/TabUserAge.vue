<template>
    <div class="tab-user-age">
        <canvas id="user-age"></canvas>
    </div>
</template>

<script>
import { Chart } from 'chart.js/auto';

export default {
    name:'TabUserAge',
    
    props:{
        userAge:Array
    },

    methods:{
        createGraph(){
            let rangeList = [];
            let connectionList = [];
            this.userAge.forEach((element) => {
                rangeList.push(element.range);
                connectionList.push(element.connections);
            });

            const ageGraph = document.getElementById('user-age');

            const createGraph = new Chart(ageGraph, {
                type:'bar',

                data:{
                    labels: rangeList,
                    datasets:[{
                        label:'',
                        data:connectionList,
                        backgroundColor: [
                            'rgba(255, 99, 132, 0.2)',
                            'rgba(255, 159, 64, 0.2)',
                            'rgba(255, 205, 86, 0.2)',
                            'rgba(75, 192, 192, 0.2)',
                            'rgba(54, 162, 235, 0.2)',
                            'rgba(153, 102, 255, 0.2)',
                            'rgba(201, 203, 207, 0.2)'
                        ],
                    }],
                },

                options:{
                    plugins:{
                        title:{
                            display:true,
                            text:'User Age Rage'
                        },
                        legend:{
                            display:false,
                        },
                    },
                    responsive:true,
                    maintainAspectRatio:false,
                }

                
            })
        }
    },

    watch:{
        userAge: {
            // Richiama la funzione createGraph quando userAge cambia - si usa per API (xchè asincrone)
            handler: 'createGraph', 
        },
    }, 
}
</script>

<style lang="scss" scoped>
div.tab-user-age{
    width: 50%;
    background-color: white;
    padding: 1rem;
    height: 30vh;
    margin-right: 1rem;
}
    
</style>