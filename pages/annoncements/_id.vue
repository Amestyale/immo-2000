<template>
  <main>
    <div class="annonce" v-if="annoncement">
      <h1>{{ annoncement.attributes.libelle }}</h1>
      <div class="annonce_content">
        <div class="annonce_carousel">
          <carousel :images="images" />
        </div>
        <div>
          <p class="annonce__price">{{ annoncement.attributes.price }} €</p>
          <p class="annonce__description">{{ annoncement.attributes.description }}</p>

          <table class="annonce_caracs">
            <tr> 
              <td> Nombre de pièces </td>
              <td> {{ pieces }} </td>
            </tr>
            <tr> 
              <td> Accès PMR </td>
              <td> {{ pmr }} </td>
            </tr>
            <tr> 
              <td> Place de parking </td>
              <td> {{ parking }} </td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import Carousel from '~/components/Carousel.vue';

export default {
  components: { Carousel },
    data() {
      return {
        annoncement : null
      }
    },
  computed: {
    images: function(){
          return this.annoncement.attributes.images.data.map(img => "http://localhost:1337" + img.attributes.url);
    },

    pieces: function(){
      return this.annoncement.attributes.pieces + " pièces" 
    },

    pmr: function(){
      return (this.annoncement.attributes.handicap_access) ? "Oui" : "Non"
    },

    parking: function(){
      return (this.annoncement.attributes.parking) ? "Oui" : "Non"
    }
  },
  mounted(){
        fetch('http://localhost:1337/graphql', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            query: `
                query{
                annoncement(id: "${this.$route.params.id}"){ 
                	data{
                    attributes{ libelle, description, price, pieces, handicap_access, parking,
                      images{data{attributes{url,alternativeText}}},
                      localisation{address,address_complement,city{data{attributes{name}}}}
                    }
                    	
                  }
                }
              }
              `,
            variables: {
            },
          }),
        })
        .then(function(response) {
          return response.json();
        })
        .then((resp) => {
            console.log(resp)
            this.annoncement = resp.data.annoncement.data
            console.log(this.annoncement)
        }); 
    }

}

</script>

<style> 
.annonce{
  margin: 0.5em 2em;
}
.annonce_content{
  display: flex;
  gap: 4em;
}
.annonce_content > * {
  flex: 1;
}
.annonce_content img{
  max-width: 100%;
}
.annonce__description{
  white-space: pre-wrap;
}
.annonce_carousel{
  height: 25em;
}
.annonce__price{
  text-align: right;
  font-weight: bold;
  font-size: 3em;
  margin: 0;
  letter-spacing: 2px;
}
.annonce_caracs{
  margin: 2em 0;
 margin-left: auto; 
}
.annonce_caracs td{
  padding: 0.25em 1em;
}
.annonce_caracs td:nth-child(1){
  font-weight: bold;
}
</style>