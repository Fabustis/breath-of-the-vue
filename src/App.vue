<template>

<div class="roboto flex flex-col xl:flex-row mx-auto justify-center container p-12 items-center">

  <div class="left flex flex-col w-full max-w-2xl mx-auto xl:w-1/2 relative xl:px-12">

    <div class="categorie flex flex-row justify-center items-center space-x-10 mb-5 mx-auto">
      <div>
        <p>Weapon</p>
        <img src="http://localhost:8080/img/categories/BotW_Weapon_Icon.png" @click="getItemByCategory('weapon')" :class="{ 'active-category': selectedCategory==='weapon'}" />
      </div>
      <div>
        <p>Shield</p>
        <img src="http://localhost:8080/img/categories/BotW_Shield_Icon.png" @click="getItemByCategory('shields')" :class="{ 'active-category': selectedCategory==='shields'}"/>
      </div>
      <div>
        <p>Armor</p>
        <img class="h-64px" src="http://localhost:8080/img/categories/BotW_Armor_Icon.png" @click="getItemByCategory('armors')"  :class="{ 'active-category': selectedCategory==='armors'}"/>
      </div>
    </div>

    <div class="flex relative itemsGrid">
        <div class="item mx-auto grid md:grid-cols-5 grid-cols-3 grid-flow-row gap-8">
            <div v-for="item in filteredItems" :key="item.id" @click="getItemById(item.id)" class="relative w-20 h-20 bg-black border-zelda-softYellow border border-opacity-50 hover:shadow-yellow hover:border-zelda-lightYellow cursor-pointer" :class="{ 'shadow-yellow' : item.id == selectedItem.id }">
                <Item :item-data="item"/>
            </div>
        </div>
    </div>

    <div class="absolute left-0 h-full items-center md:flex z-10">
      <img 
        src="./assets/arrow-no-curve.png" 
        alt="arrow previous items to left"
        class="transform rotate-180 scale-50">
    </div>
    <div class="absolute right-0 h-full items-center md:flex z-10">
      <img 
        src="./assets/arrow-no-curve.png" 
        alt="arrow previous items to right"
        class="transform scale-50">
    </div>
  
  </div>
  
  <div class="flex flex-col right items-center xl:items-start self-end w-full h-full xl:w-1/2 xl:mt-0 justify-between">

    <div class="bonus flex flex-col">
      <div class="gauges relative">
        <div class="gauge1 absolute"></div>
        <div class="gauge2 absolute"></div>
      </div>
    </div>

    <div class="item-information text-zelda-softYellow flex flex-col border-2 border-opacity-5 border-zelda-softYellow bg-black bg-opacity-5">
      <h2 class="item-information__name">{{selectedItem.name}}</h2>
      <div class="item-information__type-value flex gap-5 mt-5 mb-5">
        <img class="w-5 h-5 item-information__type" src="http://localhost:8080/img/categories/BotW_Weapon_Icon.png"/>
        <span class="item-information__value w-10 text-center border-2 border-zelda-softYellow">{{selectedItem.value}}</span>
      </div>
      <p class="item-information__description">{{selectedItem.description}}</p>
    </div>

  </div>

</div>

</template>

<script>
import ItemsJson from './assets/data/items'
import Item from './components/Item.vue'

export default {
  name: 'App',
  data(){
    return{
      items: [],
      filteredItems: [],
      selectedCategory: "shields",
      selectedItem: [],
      maxItems: [],
    }
  },
  components : {
    Item
  },
  created(){
    this.setFilteredItems();
    this.setSelectedItems();
  },
  methods:{
    setFilteredItems(){
      //Filtrage par la catégorie par défaut
      this.filteredItems = ItemsJson.filter((item) => item.category == this.selectedCategory);
    
      //on remplit les items vide pour avoir une liste de 20 max
      this.maxItems= [];
      for(var i=0;i<20-this.filteredItems.length;i++){
        this.maxItems.push({"id" : undefined})
      }
      this.filteredItems.push(...this.maxItems);
    },
    setSelectedItems(){
      //le 1er item filtré sera l'item par défaut
      this.selectedItem = this.filteredItems.filter((item) => item[0]);
    },
    getItemByCategory(val){
      this.selectedCategory=val;
      this.setFilteredItems();
    },
    getItemById(val){
      if (val !== undefined) {
        this.selectedItem = this.filteredItems.filter((item) => item.id == val);
        this.selectedItem = this.selectedItem[0];
      }
    }
  },
}

</script>

<style>

.roboto {
  font-family: 'Roboto', sans-serif;
}

.categorie {
  filter: brightness(0.5) invert(1);
}
.active-category{
  filter: brightness(0) invert(0);
}
.categorie img{
  width: 32px;
  height: 32px;
}

.categorie>div::after{
  content: "";
  width: 100%;
  height: 2px;
  background-color: rgba(255, 255, 255, 0.336);
  position: relative;
  bottom:1px;
  display: inline-block;
}

.item-information{
  padding: 10px;
}

.item-information__name{
  font-style: italic;
  font-weight: 600;
}

.gauge1 {
  display: block;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: solid 10px #03ee54;
}
.gauge2 {
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border: solid 10px #03ee54;
}

</style>