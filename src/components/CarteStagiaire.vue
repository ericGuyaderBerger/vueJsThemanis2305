<template>
    <div>
        <h2>{{ nom }}</h2>
        <div 
            id="delete"
            @click="$emit('suppression', index)"
        >x</div>
        <p>{{  organisation }}</p>
        <hr />
    </div>
</template>

<script>
export default {
    name: 'CarteStagiaire',
    props: {
        index:{
            type: Number,
            required: true,
        },
        nom : {
            type: String,
            required: true
        },
        organisation: {
            type: String,
            default: ''
        }
    },
    methods:{
        
    }
    mounted()
}
</script>

<style scoped>
div:not(#delete){
    position:relative;
    width:30em;
    border:1px solid black;
    margin:1em 0;
    padding:10px;
}
#delete{
    position: absolute;
    right:1em;
    top:0;
    cursor:pointer;
}
</style>