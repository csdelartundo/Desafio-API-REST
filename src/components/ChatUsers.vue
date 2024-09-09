<template>
    <div class="chat-content">
        <div class="user-panel left-panel">
            
            <CardUser v-if="usuarios[0]" :usuario="usuarios[0]" :esPropio="true" @enviarMensaje="enviarMensaje" />
        </div>
        <div class="chat-box">
            <div v-for="(mensaje, index) in mensajes" :key="index" class="mensaje"
                :style="{ backgroundColor: mensaje.color }" :class="mensaje.esPropio ? 'propios' : 'ajenos'">
                <strong>{{ mensaje.usuario }}:</strong> {{ mensaje.texto }}
            </div>
        </div>
        <div class="user-panel right-panel">
            
            <CardUser v-if="usuarios[1]" :usuario="usuarios[1]" :esPropio="false" @enviarMensaje="enviarMensaje" />
        </div>
    </div>
</template>

<script>
import CardUser from './CardUser.vue';

export default {
    props: {
        usuarios: Array,
        mensajes: Array,
    },
    components: {
        CardUser,
    },
    methods: {
        enviarMensaje(mensaje) {
            this.$emit('enviarMensaje', mensaje);
        },
    },
};
</script>

<style scoped>
.chat-content {
    display: flex;
    width: 80%; 
    max-width: 1200px; 
    height: 80%; 
    border: 1px solid #ddd; 
    background-color: #f9f9f9; 
}

.user-panel {
    width: 300px;
    background-color: #f8f8f8;
    padding: 10px;
    box-sizing: border-box;
}

.chat-box {
    flex: 1;
    height: 100%;
    overflow-y: auto;
    padding: 10px;
    border: 1px solid #ddd;
    background-color: #fff;
    margin: 0 10px; 
}

.mensaje {
    margin: 5px 0;
    padding: 10px;
    border-radius: 10px;
    max-width: 80%;
}

.propios {
    align-self: flex-end;
    text-align: left;
    background-color: #d6e3e8;
}

.ajenos {
    align-self: flex-start;
    text-align: right;
    background-color: #f0f0f0;
}
</style>
