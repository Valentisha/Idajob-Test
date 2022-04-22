<template>
    <div class="container-card">
        <div class="button-delete"
             @click="deleteCard"
              >
        </div>
        <div class="image-card">
          <slot  name="cardImage"></slot>
        </div>
        <div class="container-card__description">
        <h4>{{data.name}}</h4>
        <article>{{data.description}}</article>
        <div class="price">{{data.price}} руб.</div>
        </div>
    </div>
</template>

<script>
import NewCardForm from '../components/NewCardForm.vue'
import CardsContainer from '../components/CardsContainer.vue'

export default {
    components: {
    // eslint-disable-next-line
    NewCardForm,
    // eslint-disable-next-line
    CardsContainer
  },
    name: 'CardItem',

    props:[
      'data'
  ],

  methods:{
      deleteCard() {
        this.$emit('removeItem', this.data.id) 
      }
  }
}
</script>

<style lang='scss' >

.button-delete {
    background-image: url('../photo/delete.png');
    background-position: 0 0 ;
    background-repeat: no-repeat;
    width: 32px;
    height: 32px;
    background-size: 32px 32px;
    position: absolute;
    right: -9px;
    top: -9px;
    display: none;
         
}


.container-card {
    width: 100%;
    background: #FFFEFB;
    box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
    border-radius: 4px;
    cursor: pointer;
    transition: box-shadow 300ms ease;
    position: relative;

    &__description {
        padding: 16px 16px 24px 16px;
    }
}

.container-card:hover {
  box-shadow: 0px 2px 10px rgb(0 0 0 / 40%);
    .button-delete {
        display: block;
    }
}

@media (max-width: 600px) {
  .container-card {
    margin-left: 0;
    margin-bottom: 16px;
    
  }
}

h4 {
font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 600;
font-size: 20px;
line-height: 25px;
color: #3F3F3F;
margin: 0;
margin-bottom: 16px;
}

article {
font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 400;
font-size: 16px;
line-height: 20px;
color: #3F3F3F;
margin-bottom: 32px;
}

.image-card img {
    display: block;
    width: 100%;
    border-radius: 4px 4px 0 0;
}

.price {
font-family: 'Source Sans Pro';
font-style: normal;
font-weight: 600;
font-size: 24px;
line-height: 30px;
color: #3F3F3F;
}

</style>