<template>
    <div class="tab-operating-system">
        <canvas id="operating-system"></canvas>
    </div>
</template>
<script>
import { Chart } from 'chart.js/auto';

export default {
    name:'TabSystem',

    props:{
        operatingSystem: Array
    },

    methods:{
        createGraph(){
            let operetorList = [];
            let connectionList = [];
            
            this.operatingSystem.forEach((element) => {
                operetorList.push(element.os);
                connectionList.push(element.connections);
            });
            console.log(operetorList);
            console.log(connectionList);


            const systGraph = document.getElementById('operating-system');

            const systemGraph = new Chart(systGraph,{
                type:'pie',

                data:{
                    labels:operetorList,
                    datasets:[{
                        label:'torta',
                        data:connectionList,
                        backgroundColor:[
                        'rgb(255, 99, 132)',
                        'rgb(54, 162, 235)',
                        'rgb(255, 205, 86)',
                        'rgb(100, 100, 100)',
                        'rgb(200, 205, 200)',
                        ],
                        hoverOffset: 5,
                    }]
                },

                options:{
                    plugins:{
                        title:{
                            display:true,
                            text:'Operating System'
                        },
                        legend:{
                            display:true,
                            position:'right',
                            labels:{
                                padding:20,
                            }
                        }
                    },
                    responsive:true,
                    maintainAspectRatio:false,
                }  
            })
        }
    },

    watch:{
        operatingSystem: {
            // Richiama la funzione createGraph quando operatingSystem cambia - si usa per API (xchè asincrone)
            handler: 'createGraph', 
        },
    }

    
}
</script>
<style lang="scss" scoped>
div.tab-operating-system{
    width: 50%;
    background-color: white;
    padding: 1rem;
    height: 30vh;
}
    
</style>