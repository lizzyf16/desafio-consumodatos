<template>
    <div class="cardChat">
        <div v-for="(mensaje, index) in mensajes" :key="index" :style="{textAlign: mensaje.alineacion}" class="d-flex flex-column">
            <label class="fs-6"> {{ mensaje.autor }}</label>
            <div>
                <span :style="{backgroundColor: mensaje.color}" class="fs-5 rounded inline-block" id="cajaTexto">{{ mensaje.texto }}</span>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'cardChat',
    components: {
    },
    props:{
        mensajes: Array,
    },


}

</script>

<style>
.cardChat{
    background-color:rgb(216, 229, 255);
    height: 450px;
    overflow-y: scroll;
}

</style>