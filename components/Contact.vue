<template>
    <form
      @submit.prevent="submit">
      <Input v-model="mail" libelle='Your mail' name="email" placeholder="Entrez votre adresse mail" />
      <Input v-model="message" libelle='Your message' name="message" type="textarea" />
      <Input libelle='Send' type="submit"/>
    </form>
</template>


<script>
  export default {
    props: ['libelle','placeholder', 'name','type'],
    data() {
      return {
          mail : "",
          message : ""
      }
    },
    methods: {
        submit() {
            let email = this.mail
            let message = this.message
            fetch('https://formspree.io/f/mdobzrao', {
              method: 'POST',
              headers: {
                'Accept': 'application/json',
                'Content-Type': 'application/json'
              },
              body: JSON.stringify({
                  'email' : email,
                  'message' : message,
              })
            }).then(response => {
                if (response.ok) {
                  console.log("Thanks for your submission!");
                } else {
                  response.json().then(data => {
                    if (Object.hasOwn(data, 'errors')) {
                      console.log (data["errors"].map(error => error["message"]).join(", "));
                    } else {
                      console.log("Oops! There was a problem submitting your form")
                    }
                  })
                }
              }).catch(error => {
                      console.log("Oops! There was a problem submitting your form")
              });
        }
    }
  }

</script>
