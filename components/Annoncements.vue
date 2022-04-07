
<template>
  <div>
    <h1>Nos annonces</h1>
    <ul class="annonces">
      <li v-for="annoncement in annoncements" :key="annoncement.id">
        <card-annonce 
          :title="annoncement.attributes.libelle" 
          :cover="`http://localhost:1337${annoncement.attributes.images.data[0].attributes.url}`" 
          :url="`/annoncements/${annoncement.id}`" />
      </li>

    </ul>
  </div>
</template>


<script>
import CardAnnonce from './CardAnnonce.vue';

  export default {
  components: { CardAnnonce },
      data() {
        return {
          annoncements : []
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
                annoncements{ 
                	data{
                      id,
                      attributes{
                        libelle,
                        images{data{attributes{url}}
                      },
                    }}
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
          this.annoncements = resp.data.annoncements.data
          console.log(this.annoncements)
        }); 
      }
    }
</script>

<style> 
  .annonces{
    display: grid;
    grid-template-columns: repeat(3,30%);
    grid-template-rows: 20em;
    list-style: none;
  }
</style>