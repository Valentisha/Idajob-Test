<template>

<div class="grid">

    <NewCardForm @newItem='addNewItem'/>
    <CardsContainer @globalRemoveItem='removeItem' :dataItems='items'/>

</div>     
</template>

<script>
import NewCardForm from './components/NewCardForm.vue'
import CardsContainer from './components/CardsContainer.vue'


export default {
  components: {
    NewCardForm,
    CardsContainer,
    // eslint-disable-next-line
  },
   data() {
    return {
      items: 
      [
        {
        id: Date.now(),
        name: 'Наименование товара',
        description: 'Довольно-таки интересное описание товара в несколько строк. Довольно-таки интересное описание товара в несколько строк',
        link: 'https://p1.pikrepo.com/preview/900/564/white-and-black-polaroid-one-step-2-camera-on-white-table.jpg',
        price: '10 000'
       }
      ]
    }
    },
    methods: {
     addNewItem(data) {
       // eslint-disable-next-line
        this.items.push({id: Date.now(), name: data.nameItem, description: data.descriptionItem, link: data.linkItem, price: data.priceItem})
        console.log(this.items)
      },
    

     removeItem(id){
       this.items = this.items.filter((value) => {return value.id !== id}) 
     }
},
}

</script>

<style lang='scss'>

.grid {
  display: flex;
  padding: 32px 32px 0;
  background: rgba(255, 254, 251, 0.8);
}

@media (max-width: 600px) {
  .grid {
    flex-direction: column;
    width: 100%;
  }
}


</style>
