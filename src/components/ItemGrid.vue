<template>
    <div class="itemsGrid mt-10">
        <div class="item grid md:grid-cols-5 grid-cols-3 grid-flow-row gap-5">
            <div v-for="item in filteredItems" :key="item.id" @click="getItemById(item.id)" class="relative w-20 h-20 bg-black border-zelda-softYellow border-2 hover:shadow-yellow hover:border-zelda-lightYellow cursor-pointer" >
                <Item :item-data="item"/>
            </div>
        </div>
    </div>
</template>

<script>
import Item from './components/Item.vue'

export default {
    components : {
        Item
    },
    props: ['filteredItems']
}
</script>

<style>

</style>