<script setup>
import Escena from './Escena.vue'
import Botons from './Botons.vue'

import {ref,computed} from "vue";

const mostrarHistoria=ref(false);

const arrTextos=[{
    txt: "Nuestro héroe estaba flotando por el espacio sideral cuando a lo lejos divisó una nave espacial",
    img:"1.jpg"
    },
    {
    txt: "Sentía curiosidad por el interior de la nave y se puso a inspeccionarla. Llegó a una sala con dos puertas.",
    img:"2.jpg"
    },
    {
    txt: "El héroe decidió atravesar la puerta que le llevaba a casa",
    img:"3.jpg"
    },
    {
    txt: "Mientras tanto, otros héroes no tuvieron tanta suerte en su elección...",
    img:"4.jpg"
    }
];
const currentSentence=ref(0);
const backImgUrl="./img/";
const backImage=ref(backImgUrl+arrTextos[0].img);

const nextTxt=()=>{
    currentSentence.value<arrTextos.length-1 ? currentSentence.value++ : currentSentence.value=0;
    backImage.value=backImgUrl+arrTextos[currentSentence.value].img;
}
const prevTxt=()=>{
    currentSentence.value==0? currentSentence.value=arrTextos.length-1 : currentSentence.value--;
    backImage.value=backImgUrl+arrTextos[currentSentence.value].img
}

const mostrarHistoriaBtnTxt=computed(()=>{
  return currentSentence.value==0 ? "Iniciar Historia": "Continuar Historia";
})

</script>
<template>
    <div class="container">
        <div class="presentacion" v-if="!mostrarHistoria">
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem, laborum quae! Inventore maiores, earum totam nihil, iste ex laboriosam sed delectus animi autem ad corporis? Aut dignissimos totam laboriosam! Quae.</p>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quidem, laborum quae! Inventore maiores, earum totam nihil, iste ex laboriosam sed delectus animi autem ad corporis? Aut dignissimos totam laboriosam! Quae.</p>
            <button @click="mostrarHistoria = true">{{ mostrarHistoriaBtnTxt }}</button>
        </div>
        
        <div class="container__historia" :style="[{ 'background-image': 'url(' + backImage + ')' }]" v-if="mostrarHistoria">
            <div class="btn_div">
                <Botons texto="Anterior" @nextTxt="prevTxt()" /><Botons texto="Siguiente" @nextTxt="nextTxt()" />
            </div>
            <ul>
                <Escena v-for="(historia, index) in arrTextos" :indice="index" :texto=historia.txt :currentSentence=currentSentence />
                <!-- <Escena v-for="(frase, index) in arrTextos" :key="index" :texto=frase :class="{ active: index === currentSentence}" /> //También podría haberlo hecho así pero entiendo que el ejercicio pedía pasar currentSentence como prop al componente Escena-->
            </ul>
            <button @click="mostrarHistoria = false">Finalizar Historia</button>
        </div>
    </div>
</template>
<style scoped>
ul{
    list-style-type: none;
    padding: 0;
}
.btn_div{
    display: flex;

}
.presentacion{
    text-align: center;
    margin: 5rem auto;
    padding: 2rem;
    width: 80%;
    border: dotted darkcyan;
}
.container__historia{
    box-sizing: border-box;
    margin: 0;
    padding: 2rem;
    width: 100%;
    height: 100vh;
    text-align: center;
    background-size: cover;
    background-position: center;
}

p{
    margin: 2rem;
}
.container{
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 0;
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    
}
</style>
