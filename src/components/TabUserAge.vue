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
                        data:connectionList
                    }]
                },
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
}
    
</style>