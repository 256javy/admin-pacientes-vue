
<script setup>
    import { computed } from 'vue';
    const props = defineProps({
        customAlert : {
            type: Object,
            required: true
        }
    })
    const isError = computed(() => {
        return props.customAlert.type === 'error'
    })
</script>

<template>
    <div
        v-bind:class="[isError ? 'bg-red-500' : 'bg-green-500']"
        class="text-white text-center p-3 uppercase font-bold mb-3 rounded-md "
    >
        {{ customAlert.message }}
    </div>
</template>
