
<template>
    <article class="annonce_card">
      <img :src="cover" :alt="alt">
      <div class="annonce_banner">
        <NuxtLink :to="url"><h2>{{title}}</h2></NuxtLink>
      </div>
    </article>
</template>

<script>
    export default {
        props : {
            title:{
                type: String,
                required: true,
            },
            cover: {
                type: String,
                default: "https://palmares.lemondeduchiffre.fr/images/joomlart/demo/default.jpg"
            },
            url : {
                type: String,
                required: true
            }
        },
        computed: {
            alt: function(){
                return `Image de l'annonce : ${this.title}`
            }
        }
    }
</script>

<style>
    .annonce_card {
        position: relative;
        border-radius: 0.5em;
        box-shadow: 0px 4px 4px gainsboro;
        height: 100%;
        width: 100%;
        padding: 0.5em 0;
        overflow: hidden;
    }
    .annonce_card > img{    
        position: absolute;
        width: 100%;
        height: 100%;
        object-fit: cover;
        left: 0;
        top: 0;
        z-index: 1;
    }
    .annonce_card h2{    
       background-color: ghostwhite;
       padding: 0.4em;
       text-align: center;
       text-transform: capitalize;
       margin-top: 1em;
    }

    .annonce_banner{
        z-index: 2;
        position: relative;
    }
</style>