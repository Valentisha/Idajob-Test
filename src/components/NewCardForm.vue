<template>
<div class="container-modal">
    <h1> Добавление товара</h1>

    <div class="modal">

        <div :class="{
           error: !validName,
           modal__element: true, 
           required: true
             }">  
          <div class="name-title">Наименование товара</div>
          <input @input="isNameValid"
                 @blur="isNameValid"
                 class="name-input " 
                 placeholder="Введите наименование товара"
                 v-model="nameItem">
          <div v-if='!validName' 
          class="error_message"
          >Поле является обязательным</div>
        </div>


        <div class="modal__element">
          <div class="name-title ">Описание товара</div>
          <textarea class="name-input name-description" 
                    placeholder="Введите описание товара"
                    v-model="descriptionItem"
                    ></textarea>
        </div>


        <div :class="{
           error: !validLink,
           modal__element: true, 
           required: true
             }">
          <div class="name-title">Ссылка на изображение товара</div>
          <input @blur="isLinkValid"
                 @input="isLinkValid"
                 class="name-input" 
                 placeholder="Введите ссылку"
                 v-model="linkItem"   >
          <div v-if='!validLink' 
          class="error_message"
          >Поле является обязательным</div>
        </div>


        <div :class="{
           error: !validPrice,
           modal__element: true, 
           required: true
             }">
          <div class="name-title">Цена товара</div>
          
          <input 
          @blur="isPriceValid"
          @input="isNumberSplit"       
                 class="name-input" 
                 placeholder="Введите цену"
                 v-model="priceItem" >
          <div v-if='!validPrice' 
          class="error_message"
          >Поле является обязательным</div>
        </div>

        <button :class="{
                modal_button: true,
                modal_buttonactive: isFormValid}"
                @click='addItem'
        >Добавить товар</button>
         <!-- @click="addNewItem" -->
         

     </div>
</div>
</template>

<script>
export default {
  name: 'NewCardForm',
  
  data() {
    return {

      validName: true,
      validLink: true,
      validPrice: true,
    
  
      nameItem: '',
      descriptionItem: '',
      linkItem: '',
      priceItem: '0'
    
    }
  },

  computed: {
    // eslint-disable-next-line
    isFormValid() {
      
      if (this.nameItem.length > 0 &&
      this.linkItem.length > 0 &&
       Number(this.priceItem.split(' ').join('')) > 0){
        // eslint-disable-next-line
        return true
      } else {
        return false
      }
      
    }
  },

  methods: {

    isNumberSplit(){
 
      let currentPrice = Number(this.priceItem.split(' ').join(''));
      this.priceItem = Intl.NumberFormat('ru-RU').format(currentPrice);
      

            if (this.priceItem.length > 0){
          this.validPrice = true
      } else {
        this.validPrice = false
      }
    },
  

    isNameValid(){
      if (this.nameItem.length > 0){
          this.validName = true
      } else {
        this.validName = false
      }
    },

    isLinkValid(){
      if (this.linkItem.length > 0){
          this.validLink = true
      } else {
        this.validLink = false
      }
    },

    isPriceValid(){
      if ( Number(this.priceItem.split(' ').join('')) > 0){
          this.validPrice = true
      } else {
        this.validPrice = false
      }
    },
   
    addItem(){

      this.isNameValid()
      this.isLinkValid()
      this.isPriceValid()
      if (this.isFormValid === true){
        // eslint-disable-next-line 
        this.$emit('newItem', {nameItem: this.nameItem, descriptionItem: this.descriptionItem, linkItem: this.linkItem, priceItem: this.priceItem})
      }
    },
     
 
  }
}
</script>

<style lang='scss'>

    body {
      margin: 0;
    }


    .error {
      .name-input{
            border: 1px solid rgba(255, 132, 132, 1);
          }
     
    }


    .error_message {
      font-family: 'Source Sans Pro';
      font-style: normal;
      font-weight: 400;
      font-size: 8px;
      line-height: 10px;
      letter-spacing: -0.02em;
      color: #FF8484;
      margin-top: 4px;
      display: block;
    
    }

    h1 {
      font-family: 'Source Sans Pro';
      font-weight: 600;
      font-size: 28px;
      line-height: 35px;
      color: #3F3F3F;
      margin: 0;
      margin-bottom: 16px;
    }
    @media (max-width: 600px) {
    h1 {
    text-align: center;
  
    
  }
}

    .container-modal{ 
      display: block;
    }
    
    
    .modal {
      margin: 0 auto;
      width: 332px;
      padding: 24px;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      background: #FFFEFB;
    
    
      &__element {
        margin-top: 16px;
        &:first-child {
          margin-top: 0;
        }
      }
    }

    @media (max-width: 600px) {
  .modal {
    width: auto;
    
  }
}

    
    
  .modal_button {
    width: 100%;
    height: 36px;
    background: #EEEEEE;
    border-radius: 10px;
    border: none;
    margin-top: 24px;
    font-family: 'Inter';
    font-style: normal;
    font-weight: 600;
    font-size: 12px;
    line-height: 15px;
    text-align: center;
    letter-spacing: -0.02em;
    color: #B4B4B4;
    cursor: pointer;
    
  }

    .modal_buttonactive{
      background: #7BAE73;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
      color: #FFFFFF;
     
    }

    .name-title {
      font-family: 'Source Sans Pro', sans-serif;
      font-style: normal;
      font-weight: 400;
      font-size: 10px;
      line-height: 13px;    
      letter-spacing: -0.02em;
      color: #49485E;
      margin-bottom: 4px;
    
      
    }
    
    .required {
      .name-title {
        &::after {
        content: "";
        background-image: url('../photo/circle.png');
        background-position: 0 0 ;
        background-repeat: no-repeat;
        width: 4px;
        height: 4px;
        display: inline-block;
        background-size: 4px 4px;
        margin-bottom: 5px;
        }}
      }
    
    
    .name-input {
      width: 100%;
      height: 36px;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      font-family: 'Source Sans Pro', sans-serif;
      font-weight: 400;
      font-size: 12px;
      line-height: 15px;
      border: none;
      color: #B4B4B4;
      opacity: 1;
      box-sizing: border-box;
      padding-left: 16px;
     
    }

    
    
    ::placeholder {
      color: #B4B4B4;
      opacity: 1;
    }
    
    .name-description {
      width: 100%;
      height: 108px;
      background: #FFFEFB;
      box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
      border-radius: 4px;
      font-weight: 400;
      font-size: 12px;
      line-height: 15px;
      
      resize: none;
      padding-top: 10px;
     
    }
    
    </style>