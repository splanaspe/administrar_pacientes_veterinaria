<script setup>
// Import Vue Composition API hooks and other stuff here
    import { ref, onMounted, reactive, computed} from 'vue'
    import Alerta from './Alerta.vue';
    const alerta = reactive({
        tipo: '',
        mensaje: ''
    })

    const editando = computed( () => {
        return props.id
    })

    const validarFormulario = () =>{
        if (Object.values(props).includes('')){
            console.log("Formulario vacio")
            alerta.tipo="error";
            alerta.mensaje="Todos los campos son obligatorios";
            return;
        }
        emit('guardar-paciente')
        alerta.tipo="exito"
        alerta.mensaje="Paciente añadido correctamente"

        setTimeout( () => {
            Object.assign(alerta, {
                mensaje: '',
                tipo: ''
            })
        },3000)
        
    }

    const emit = defineEmits([
        'update:nombre',
        'update:propietario',
        'update:alta',
        'update:email',
        'update:sintomas',
        'guardar-paciente'
    ]);

    const props = defineProps({
        id:{
            type: [String,null],
            required:true
        },
        nombre:{
            type: String,
            required: true
        },
        propietario:{
            type: String,
            required: true
        },
        email:{
            type: String,
            required: true
        },
        alta:{
            type: String,
            required: true
        },
        sintomas:{
            type: String,
            required: true
        }
    })


</script>
<template>
    <div class="md:w-1/2 mx-2"> 
        <h2 class="font-black text-3xl text-center"> Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10"> 
            Añade Pacientes y 
            <span class="text-indigo-600 font-bold"> Adminístralos</span>
        </p>
        <Alerta 
            v-if="alerta.mensaje"
            :alerta="alerta"
        />
        <form 
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent = "validarFormulario"
        >
            
            <div class="mb-5"> 
                <label
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold"
                > 
                    Nombre Mascota
                </label>
                <input
                    id="mascota"
                    type="text"
                    placeholder="nombre de la mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="nombre"
                    @input="$emit('update:nombre', $event.target.value)"
                /> 
            </div>
            <div class="mb-5"> 
                <label
                    for="propietario"
                    class="block text-gray-700 uppercase font-bold"
                > 
                    Nombre propietario
                </label>
                <input
                    id="propietario"
                    type="text"
                    placeholder="nombre del propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="propietario"
                    @input="$emit('update:propietario', $event.target.value)"
                    /> 
            </div>
            <div class="mb-5"> 
                <label
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                > 
                    Email
                </label>
                <input
                    id="email"
                    type="email"
                    placeholder="email"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="email"
                    @input="$emit('update:email', $event.target.value)"
                    /> 
            </div>
            <div class="mb-5"> 
                <label
                    for="alta"
                    class="block text-gray-700 uppercase font-bold"
                > 
                    alta
                </label>
                <input
                    id="alta"
                    type="date"
                    placeholder="alta"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    :value="alta"
                    @input="$emit('update:alta', $event.target.value)"
                    /> 
            </div>
            <div class="mb-5"> 
                <label
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold"
                > 
                    Síntomas
                </label>
                <textarea
                    id="sintomas"
                    placeholder="Descríbe los síntomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    :value="sintomas"
                    @input="$emit('update:sintomas', $event.target.value)"
                    /> 
            </div>
            <input
                type="submit"
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-700 cursor-pointer transition-colors"
                :value="[editando ? 'Guardar Cambios' : 'Registrar Paciente']"
            /> 
        </form>
    </div>
</template>
<style scoped>

</style>