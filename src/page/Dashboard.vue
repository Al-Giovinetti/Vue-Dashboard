<template>
    <body>
        <Navbar />
        <main>
            <TabMonthlyConnection :monthlyConnection="dataForTable.MonthlyConnections" />
            <div class="second-row">
                <TabUserAge :userAge="dataForTable.UsersAgeRange" />
                <TabSystem :operatingSystem="dataForTable.Devices" />
            </div>
        </main>
    </body>
</template>
<script>
import axios from "axios"
import Navbar from "../components/Navbar.vue"
import TabMonthlyConnection from "../components/TabMonthlyConnection.vue"
import TabUserAge from "../components/TabUserAge.vue"
import TabSystem from "../components/TabSystem.vue"

export default {
    name:"Dashboard",

    components:{
        Navbar,
        TabMonthlyConnection,
        TabUserAge,
        TabSystem,
    },

    data(){
        return{
            urlDataForTable:'https://file.notion.so/f/s/f653ce74-5a61-4176-9bbf-b8acb3e5927b/data.json?id=90a8bbbb-46be-47a2-be85-b126c5911cab&table=block&spaceId=4c49ff97-016b-4669-8de5-4479dd1a86e1&expirationTimestamp=1699725600000&signature=thnVR5zlUcWfPTp0LBH9pjpIPYNaYr0dxpfp_u-uaHQ&downloadName=data.json',
            dataForTable:[],
        }
    },

    methods:{
        getTableList(){
            axios.get(this.urlDataForTable).then((response) => {
                // handle success
                console.log(response.data);
                this.dataForTable = response.data
            })
            .catch(function (error) {
                // handle error
                console.log('Errore nella richiesta API', error);
            })
        }
    },

    created(){
        this.getTableList()
    }
}
</script>
<style lang="scss" scoped>
    main{
        width: 80vw;
        background-color: yellow;
        padding: 1rem;
    }
    div.second-row{
        display: flex;
        justify-content: center;
        margin-top: 1rem;
    }
</style>