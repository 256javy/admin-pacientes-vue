<script setup>
    import {computed, reactive} from 'vue'
    import Alert from './Alert.vue'

    const props = defineProps({
        id : {
            type: [String, null],
            required: true
        },
        name : {
            type: String,
            required: true
        },
        owner : {
            type: String,
            required: true
        },
        email : {
            type: String,
            required: true
        },
        patientDischarge : {
            type: String,
            required: true
        },
        symptoms : {
            type: String,
            required: true
        },
    })

    const emit = defineEmits([
        'update:name',
        'update:owner',
        'update:email',
        'update:patientDischarge',
        'update:symptoms',
        'save-pet'
    ])

    const customAlert = reactive({
        type: '',
        message: '',
    })



    const validate = (e) =>{
        if(Object.values(props).includes('')){
            customAlert.message = "Todos los campos son requeridos"
            customAlert.type = 'error'
            
        } else {
            customAlert.message = "Gaurdado correctamente"
            customAlert.type = 'success'
            emit('save-pet')
        }
        setTimeout( () => {
            customAlert.message = ''
        }, 3000)
        
    }

    const editing = computed(() => props.id)

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="font-bold text-indigo-600">Adminístralos</span>
        </p>

        <Alert
            v-if="customAlert.message"
            v-bind:customAlert="customAlert"
        />

        <form 
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            v-on:submit.prevent="validate"
        >
            <div class="mb-5">
                <label for="name" class="block text-gray-700 uppercase font-bold">
                    Nombre Mascota
                </label>
                <input 
                    type="text" 
                    id="name" 
                    placeholder="Nombre de la mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-bind:value="name"
                    @input="$emit('update:name', $event.target.value)"
                >
            </div>
            <div class="mb-5">
                <label for="owner" class="block text-gray-700 uppercase font-bold">
                    Nombre Propietario
                </label>
                <input 
                    type="text" 
                    id="owner" 
                    placeholder="Nombre del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-bind:value="owner"
                    @input="$emit('update:owner', $event.target.value)"
                >
            </div>
            <div class="mb-5">
                <label for="email" class="block text-gray-700 uppercase font-bold">
                    Email
                </label>
                <input 
                    type="email" 
                    id="email" 
                    placeholder="Email del Propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-bind:value="email"
                    @input="$emit('update:email', $event.target.value)"
                >
            </div>
            <div class="mb-5">
                <label for="patientDischarge" class="block text-gray-700 uppercase font-bold">
                    Alta
                </label>
                <input 
                    type="date" 
                    id="patientDischarge" 
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    v-bind:value="patientDischarge"
                    @input="$emit('update:patientDischarge', $event.target.value)"
                >
            </div>
            <div class="mb-5">
                <label for="symptoms" class="block text-gray-700 uppercase font-bold">
                    Síntomas
                </label>
                <textarea 
                    id="symptoms" 
                    placeholder="Describe los Síntomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    v-bind:value="symptoms"
                    @input="$emit('update:symptoms', $event.target.value)"
                ></textarea>
            </div>

            <input 
                type="submit" 
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold rounded-md hover:bg-indigo-700 cursor-pointer transition-colors"
                v-bind:value="[editing ? 'Guardar Cambios' : 'Registrar Paciente']"
                >

        </form>
    </div>
</template>
