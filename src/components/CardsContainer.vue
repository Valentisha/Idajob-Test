<template>
<div class="container-page">
    <select name="#" id="#" class="list">
        <option value="#">По умолчанию</option>\
    </select>
<div class="cards">

 <CardItem 
  @removeItem='removeItem'
  :data="item" 
  v-for="item in dataItems" 
  :key="item.id">

    <template #cardImage>
    <img :src='item.link'/> 
    </template>
 </CardItem>


 

</div>

</div>
</template>

<script>
import CardItem from './CardItem.vue'


export default {
    components: {
    CardItem  
    },
    name: 'CardsContainer',
   
    props:[
      'dataItems',
  ],
    emits: {
       // eslint-disable-next-line
      globalRemoveItem (payload) {
        return true
      }
    },

    methods: {
      removeItem(id){ 
        this.$emit('globalRemoveItem', id)
      }
    }
    }
</script>

<style lang='scss' scoped>

.cards {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
    width: 100%;
    padding-left: 16px;
}
@media (max-width: 600px) {
  .cards {
    flex-direction: column; 
    display: flex; 
    padding-left: 0;
  }
}

.list {
font-family: 'Source Sans Pro';
font-weight: 400;
font-size: 12px;
line-height: 15px;
color: #B4B4B4;
padding: 10px 27.5px 11px 16px;
background: #FFFEFB;
box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
border-radius: 4px;
border: none;
margin-bottom: 16px;
margin-left: auto;
display: block;
}

@media (max-width: 600px) {
  .list {
    margin-top: 16px;  
  }
}
</style>