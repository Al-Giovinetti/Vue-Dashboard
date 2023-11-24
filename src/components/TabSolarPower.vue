<template>
    <section class="solar-power">
        <button class="play" @click="addElement()">Start</button>
        <div class="table-solar">
            <canvas id="solar-power"></canvas>
        </div>
        {{ axeY }}
    </section>
</template>
<script>
import { Chart } from 'chart.js/auto';

export default {
    name:'TabSolarPower',

    data(){
        return{
            axeY:[],
        }
    },

    props:{
       solarData:Array,
    },

    methods:{
        createdGraph(){
            console.log('grafico creato');
            const solarGraph = document.getElementById('solar-power');
            let y=this.axeY;
            console.log(y);
            let houers=[1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24];
            const newGraph = new Chart(solarGraph,{
                type:'line',
                data:{
                    labels:  houers,
                    datasets:[{
                        label:'Daily',
                        data:y,
                        backgroundColor: 'rgb(54, 162, 235)',
                        fill:'start',
                        tension:0.5,
                    }]
                },
                options:{
                    scales:{
                        y:{
                            beginAtZero:true,
                            min: 0,
                            max: 100,
                        },
                    },
                    responsive:true,
                    maintainAspectRatio: false,
                },
                
            })
        },

        addElement(){
            let oldArray=this.solarData;
            if(oldArray.length>0){
                let moveElement= oldArray.shift();
                this.axeY.push(moveElement);
                console.log(this.axeY);

                this.updateGraph();
            }
        },

        updateGraph() {
        // Chiamato per aggiornare il grafico con i dati più recenti
        const solarGraph = document.getElementById('solar-power');
        solarGraph.data.datasets[0].data = this.axeY;
        solarGraph.update();  // Aggiorna il grafico
        },
    },

    mounted(){
        this.createdGraph();
    },

    /*watch: {
        axeY: {
            // Richiama la funzione createGraph quando monthlyConnection cambia - si usa per API (xchè asincrone)
            handler: 'createdGraph', 
        },
    },*/   
}
</script>
<style lang="scss" scoped>
    section.solar-power{
        text-align: center;
        background-color: white;
        margin-top: 1rem;
    }

    button{
        margin: 1rem;
        padding: 0.5rem;
        box-shadow: 5px 3px 5px;
        font-family: 'Roboto', sans-serif;
        background-color: rgb(135, 87, 255);
        border: 0;
        border-radius: 14px;
    }

    .table-solar{
        height: 30vh;
        padding: 1rem;
    }

    #table-solar{
        margin: auto;
        width: 100%;
        padding: 1rem;
    }
</style>