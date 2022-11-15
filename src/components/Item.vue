<template>
    <div v-if="itemData.src">
        <img  :src="'http://localhost:8080/img/'+itemData.src"/>
        <span class="absolute text-white italic right-1 bottom-1 bg-black">{{itemData.value}}</span>
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: ['itemData']
}
</script>

<style>
</style>