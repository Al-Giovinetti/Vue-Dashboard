<template>
    <body>
        <Navbar />
        <main>
            <TabMonthlyConnection :monthlyConnection="dataForTable.MonthlyConnections" />
            <div class="second-row">
                <TabUserAge :userAge="dataForTable.UsersAgeRange" />
                <TabSystem :operatingSystem="dataForTable.Devices" />
            </div>
            <TabSolarPower :solarData="solarPower"/>
        </main>
    </body>
</template>
<script>
import axios from "axios"
import Navbar from "../components/Navbar.vue"
import TabMonthlyConnection from "../components/TabMonthlyConnection.vue"
import TabUserAge from "../components/TabUserAge.vue"
import TabSystem from "../components/TabSystem.vue"
import TabSolarPower from "../components/TabSolarPower.vue"

export default {
    name:"Dashboard",

    components:{
        Navbar,
        TabMonthlyConnection,
        TabUserAge,
        TabSystem,
        TabSolarPower,
    },

    data(){
        return{
            urlDataForTable:'https://file.notion.so/f/f/4c49ff97-016b-4669-8de5-4479dd1a86e1/f653ce74-5a61-4176-9bbf-b8acb3e5927b/data.json?id=90a8bbbb-46be-47a2-be85-b126c5911cab&table=block&spaceId=4c49ff97-016b-4669-8de5-4479dd1a86e1&expirationTimestamp=1700928000000&signature=Z7HXfGJw0IE0b7zEa9HTow5y4s3J5wLsnsz6bZ50jVk&downloadName=data.json',
            dataForTable:[],

            solarPower:[5, 9, 12, 15, 20, 30, 35, 40, 50, 70, 80, 87, 90, 87, 82, 75, 60, 58, 45, 40, 21, 18, 10, 3],
        }
    },

    methods:{
        getTableList(){
            axios.get(this.urlDataForTable).then((response) => {
                // handle success
                //console.log(response.data);
                this.dataForTable = response.data
            })
            .catch(function (error) {
                // handle error
                console.log('Errore nella richiesta API', error);
            })
        },
    },

    created(){
        this.getTableList()
    }
}
</script>
<style lang="scss" scoped>
    main{
        width: 85vw;
        background-color: rgb(255, 255, 0);
        padding: 1rem;
    }
    div.second-row{
        display: flex;
        justify-content: center;
        margin-top: 1rem;
    }
</style>