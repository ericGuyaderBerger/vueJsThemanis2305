<template>
  <!-- Afficher cette variable dans un paragraphe-->
   <p :class="nomClasse" v-if=" message  ">{{ messageEnMajuscules }}</p>
   <span v-else>Je n'ai pas de message à afficher</span>

   <p class="form">
    <input type="text" placeholder="Votre message" v-model="message">
    <button @click="changerClasse">Changer état</button>
    </p>

    <p v-if="todos">{{ todos.length }}</p>
    
    <carte-slots  
      v-for="(stagiaire,index) in stagiaires" 
      :key="index" 
      :fermable="fromThemanis(stagiaire)"
      @suppression="supprimer($event)"
    >
      <template #titre>

        {{ stagiaire.nom }}
      </template>
      {{ stagiaire.employeur}}
      <template v-if="fromThemanis(stagiaire)" #pied="vientDuPied">
        Formateur {{ vientDuPied.nom }}
      </template>
    </carte-slots>
</template>

<script>
import CarteSlots from "@/components/CarteAvecSlots.vue"
import axios from 'axios'

export default {
  components: {
    CarteSlots
  },
  data(){
    // Variables internes de la vue (état applicatif limité à la vue)
    return {
      // définir une variale interne à la Vue (message)
      message: null,
      nomClasse: 'on',
      stagiaires: [
        { 
          nom: 'Matéo',
          employeur:'CHU 31'
        },
        { 
          nom: 'Frédéric',
          employeur:'CHU 31'
        },
        { 
          nom: 'Julien',
          employeur:'INRAE'
        },
        { 
          nom: 'Eric',
          employeur:'Thémanis'
        },
      ],
      todos: null,
    }
  },
  computed: {
    //Propriétés calculées
    messageEnMajuscules(){
      return this.message.toUpperCase();
    },
    
  },
  watch: {
    // Watchers de l'instance
    message(val){
      console.log(val);
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
    },
    supprimer(index){
      this.stagiaires.splice(index,1);
    },
    fromThemanis(person) {
      const result = !! person.employeur.match(/^th[eé]manis$/i) 
      console.log(person, result);
      return result;
    }
  },
  created(){
    axios
      .get('https://my-json-server.typicode.com/vuejstrainings/todosListDb/todos')
      .then( res => {
        this.todos = res.data;
      })
      .catch( err => console.log(err) )
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
