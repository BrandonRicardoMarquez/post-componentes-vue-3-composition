<script setup>
    // const props = defineProps(["title", "id", "body", "colorText"])
    // console.log(props.title)
    // console.log(props.id)
    // console.log(props.body)
    // console.log(props.colorText)
defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripción', 
        },
    });
const emit = defineEmits(['cambiarFavoritoNombre'])

//emit('cambiarFavoritoNombre', title)
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title">
                <!-- :class="`text-${colorText}`"  -->
                {{ id }} - {{ title }}
            </h5>
            <p>{{body}}</p>
            <!-- <button @click="$emit('cambiarFavoritoNombre', title)"  class="btn btn-outline-primary">😁</button> -->
            <button @click="emit('cambiarFavoritoNombre', title)"  class="btn btn-outline-primary">😁</button>
        </div>
    </div>
</template>