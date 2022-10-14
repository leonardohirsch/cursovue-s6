<script setup>
// const props=defineProps({
//     texto:{
//         type: String
//     },
//     clase:{
//         type: String
//     }
// }) //También podría haberlo hecho así pero entiendo que el ejercicio pedía pasar currentSentence como prop al componente Escena
const props=defineProps({
    texto:{
        type: String
    },
    currentSentence:{
        type: Number
    },
    indice:{
        type: Number
    }
})
</script>
<template>
    <!-- <li :class=clase>{{ texto }}</li> //También podría haberlo hecho así pero entiendo que el ejercicio pedía pasar currentSentence como prop al componente Escena--> 
    <li :class="{ active: indice === currentSentence}">{{ texto }}</li>
</template>
<style scoped>
li {
    border: solid;
    border-radius: 10px;
    margin: 2rem;
    padding: 0.3rem;
    text-align: center;
    background: rgba(249, 239, 239, 0.8);
}
.active{
    font-weight: bold;
    background-color: rgb(250, 128, 114, 0.9);
}
</style>
