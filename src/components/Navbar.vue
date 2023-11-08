<template>
    <section>
        <h1>- Dashbool -</h1>
        <div class="user-info">
            <div class="user-image">
                image
            </div>
            <div class="user-name">
                <p>Welcome</p>
                <p>Mario Rossi</p>
            </div>
        </div>
        <h2>general</h2>
        <div class="bar">-------------------------------------------</div>
        <nav>
            <ul>
                <li v-for="element in navElements">
                    <i :class="element.icon" class="myIcon"></i>
                    <a href="">{{ element.name }}</a>
                    <i class="fa-solid fa-chevron-down opening-arrow" @click="element.clicked = !element.clicked"></i>
                    <ul v-if="element.clicked == true" >
                        <li v-for="elementChild in element.childs">
                            {{ elementChild }}
                        </li>
                    </ul>
                </li>
            </ul>
        </nav>
    </section>
</template>

<script>
export default {
    name:"NavBar",

    data(){
        return{
            navElements:[
                {
                    name:'Home',
                    icon:'fa-solid fa-house',
                    childs:['Home1','Home2','Home3'],
                    clicked:false
                },
                {
                    name:'Maps',
                    icon:'fa-solid fa-map-location-dot',
                    childs:['Maps1','Maps2','Maps3'],
                    clicked:false,
                },
                {
                    name:'Config',
                    icon:'fa-solid fa-gear',
                    childs:['Config1','config2','Config3'],
                    clicked:false,
                },
                {
                    name:'Contacts',
                    icon:'fa-solid fa-envelope',
                    childs:['Contacts1','Contacts2','Contacts3'],
                    clicked:false,
                },
            ],
        }
    },

    methods:{
        openNavElement(isClicked) {
            isClicked = !isClicked
            console.log(isClicked)
            return isClicked
        },
    }
    
}
</script>

<style lang="scss" scoped>
    section{
        width: 20vw;
        background: red;
        padding: 1rem;
    }
    div.user-info{
        display: flex;
        padding: 0.5rem 0;

        .user-image{
            margin-right: 1rem;
        }
    }

    nav li{
        list-style-type: none;
        padding: 0.5rem 0;
        .myIcon{
            margin-right: 10px;
            height: 10px;
        }

        a{
            text-decoration: none;
            color: black;
        }
        .opening-arrow{
            float: right;
        }
    }
</style>