<template>
    <ul>
        <li v-for="option in props.questionOptions" :key="option.id">
            <input type="radio" name="name" :id="option.id" @click="$emit('emit-selection', option.value)"  />
            <span>{{ option.value }}</span>
        </li>
    </ul>
</template>

<script setup>
const props = defineProps({
    questionOptions: {
        type: Array,
        required: true
    }
})
defineEmits(['emit-selection'])
</script>

<style scoped>
li{
    padding: 0px 0 10px 0px;
}
</style>