<template>
    <body>
        <Navbar />
        <main>
            main
        </main>
    </body>
</template>
<script>
import Navbar from "../components/Navbar.vue"

export default {
    name:"Dashboard",

    components:{
        Navbar
    },

    data(){
        return{

        }
    }
}
</script>
<style lang="scss" scoped>
    main{
        width: 80vw;
        background-color: yellow;
    }
</style>