<template>
    <div class="cardUsuario">
        <div class="caja">
            <img class="rounded" :src="imagenUsuario">
            <p> {{ nombre }}</p>
            <div >
                <form class="d-flex flex-column gap-1" @submit.prevent="enviarMsg">
                    <input class="inputColor " type="color" name="" id="" v-model="colorFondo">
                    <textarea name="" id="" v-model="textoChat" @keyup.enter="enviarMsg" rows="5"></textarea>
                    <button class="btn btn-info">Enviar</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: 'cardUsuario',
    components: {
    },
    props: {
        imagenUsuario: String,
        nombre: String,
        alineacion: String
    },
    data() {
        return {
            colorFondo: "#aa5588",
            textoChat: "",
        }
    },
    methods: {
        enviarMsg: function () {
            let mensaje = {
                autor: this.nombre,
                color: this.colorFondo,
                texto: this.textoChat,
                alineacion: this.alineacion

            }
            if (this.textoChat.length > 0 && this.textoChat != "\n") {
                this.$emit("enviarChat", mensaje)
            }
            this.textoChat = ""
        }
    }

}

</script>

<style>
.cardUsuario{
    
    width: 100%;
}
.caja {
    display: block;
    justify-content: center;
    text-align: center;
}
.inputColor{
    width: 100%;
}
</style>