<template>
  <!-- Afficher cette variable dans un paragraphe-->
   <p :class="nomClasse" v-if=" message  ">{{ messageEnMajuscules }}</p>
   <span v-else>Je n'ai pas de message à afficher</span>

   <p class="form">
    <input type="text" placeholder="Votre message" v-model="message">
    <button @click="changerClasse">Changer état</button>
    </p>
</template>

<script>
export default {
  // définir une variale interne à la Vue (message)
  data(){
    // Variables internes de la vue (état applicatif limité à la vue)
    return {
      message: null,
      nomClasse: 'on'
    }
  },

  computed: {
    //PRopriétés calculées
    messageEnMajuscules(){
      return this.message.toUpperCase();
    }
  },
  methods:{
    // Actions/Opérations de la vue
    changerClasse(){
      // pourpouvoir accéder à un autre élément constitutif de l'instance de Vue
      // utiliser this
      if( this.nomClasse == 'on') {
        this.nomClasse = 'off';
      }else{
        this.nomClasse = 'on';
      }

      // this.nomClasse = ( this.nomClasse == 'on' ) ? 'off' : 'on';
    }
  }
}

</script>

<style scoped>
.on {
  color: black;
}

.off{
  color:#aaa
}
</style>
