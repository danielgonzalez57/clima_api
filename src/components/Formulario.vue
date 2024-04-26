<script setup>
    import {reactive, ref} from 'vue'
    import Alert from './Alert.vue'

    const busqueda = reactive({
        ciudad: '',
        pais: ''
    })

    const emit = defineEmits(['obtener-clima']);

    const error = ref('')

    const paises = [
        { codigo: 'US', nombre: 'Estados Unidos'},
        { codigo: 'MX', nombre: 'México' },
        { codigo: 'AR', nombre: 'Argentina' },
        { codigo: 'CO', nombre: 'Colombia' },
        { codigo: 'CR', nombre: 'Costa Rica' },    
        { codigo: 'ES', nombre: 'España' },
        { codigo: 'PE', nombre: 'Perú' }
    ]

    const consultarClima = () => {
        if(Object.values(busqueda).includes('')){
            error.value = 'Todos los campos son obligatorios'
            return
        }
        error.value = ''
        emit('obtener-clima', busqueda);
    }
</script>

<template>
    <form 
        class="formulario"
        @submit.prevent="consultarClima"
    >
        <Alert v-if="error">{{ error }}</Alert>
        <div class="campo">
            <label for="ciudad">Ciudad</label>
            <input 
                type="text" 
                id="ciudad"
                placeholder="Ciudad"
                v-model="busqueda.ciudad"
            >
        </div>
        <div class="campo">
            <label for="ciudad">Ciudad</label>
            <select 
                type="text" 
                id="ciudad"
                placeholder="Ciudad"
                v-model="busqueda.pais"
            >
                <option value="">-- Seleccione un pais --</option>
                <option v-for="pais in paises" :value="pais.codigo">{{ pais.nombre }}</option>
            </select>
        </div>

        <input type="submit" value="Consultar Clima">

    </form>
</template>