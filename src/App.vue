<script setup>
    import {ref, reactive, onMounted, watch} from 'vue'
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

    watch(pets, () => {
        saveInLocalStorage()
    },{
        deep: true
    })

    onMounted(() => {
        const petsFromLocalStorage = localStorage.getItem('pets')
        if(petsFromLocalStorage){
            pets.value = JSON.parse(petsFromLocalStorage)
        }

    })

    const saveInLocalStorage = () => {
        localStorage.setItem('pets', JSON.stringify(pets.value))
    }

    const savePet =  () => {
        if(pet.id){
            const {id} = pet
            const i = pets.value.findIndex((value, index) => value.id === id)
            pets.value[i] = {...pet}
        }else{
            console.log("nuevo")
            pets.value.push({
                ...pet,
                id : uid()
            })
        }
        Object.assign(pet, {
            name : '',
            owner : '',
            email : '',
            patientDischarge : '',
            symptoms : '',
            id: null
        })
    }

    const loadPet = (id) => {
        const toEdit = pets.value.filter(p => p.id === id)[0]
        Object.assign(pet, toEdit)
    }

    const deletePet = (id) => {
        pets.value = pets.value.filter(pet => pet.id !== id)
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
                v-bind:id="pet.id"
                
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
                        @load-pet="loadPet"
                        @delete-pet="deletePet"
                    />
                </div>
                <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>

            </div>
        </div>
    </div>
</template>
