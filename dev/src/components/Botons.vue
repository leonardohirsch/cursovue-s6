<script setup>
const props=defineProps({
    texto:{
        type: String
    }
})

const emit=defineEmits(["nextTxt"]);
</script>
<template>
    <button @click="$emit('nextTxt')">{{ texto }}</button>
</template>
<style scoped>
button {
   width: 100%;
   margin: 0 2rem;
}
</style>