<script setup>
    import {reactive} from 'vue'

    const pet = reactive({
        name : '',
        owner: '',
        email: '',
        patientDischarge: '',
        symptoms: ''
    })

    const validate = (e) =>{
        
        console.log(window)
    }

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>

        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="font-bold text-indigo-600">Adminístralos</span>
        </p>

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
                    v-model="pet.name"
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
                    v-model="pet.owner"
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
                    v-model="pet.email"
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
                    v-model="pet.patientDischarge"
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
                    v-model="pet.symptoms"
                >
                </textarea>
            </div>

            <input 
                type="submit" 
                class="bg-indigo-600 w-full p-3 text-white uppercase font-bold rounded-md hover:bg-indigo-700 cursor-pointer transition-colors"
                value="Registrar Paciente"
                >

        </form>
    </div>
</template>
