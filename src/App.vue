<script setup>
    import {ref, reactive} from 'vue'
    import {uid} from 'uid'
    import Header from './components/Header.vue';
    import Form from './components/Form.vue';
    import Pet from './components/Pet.vue';


    const pets = ref([])

    const pet = reactive({
        id: null,
        name: '',
        owner: '',
        email: '',
        patientDischarge: '',
        symptoms: ''
    })

    const savePet =  () => {
        pets.value.push({
            ...pet,
            id : uid()
        })
        pet.name = ''
        pet.owner = ''
        pet.email = ''
        pet.patientDischarge = ''
        pet.symptoms = ''
    }
    
</script>

<template>
    <div class="container mx-auto mt-20">
        <Header />

        <div class="mt-12 md:flex">
            <Form
                v-model:name="pet.name"
                v-model:owner="pet.owner"
                v-model:email="pet.email"
                v-model:patientDischarge="pet.patientDischarge"
                v-model:symptoms="pet.symptoms"
                @save-pet="savePet"
             />

            <div class="md:w-1/2 md:h-screen overflow-y-scroll">
                <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>

                <div v-if="pets.length > 0" class="" >
                    <p class="text-lg mt-5 text-center mb-10">
                        Información de 
                        <span class="font-bold text-indigo-600">Pacientes</span>
                    </p>
                    <Pet
                        v-for="p in pets"
                        :p="p"
                    />
                </div>
                <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>

            </div>
        </div>
    </div>
</template>
