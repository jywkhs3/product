<template>
  <div class="cart">
    <OpenModal :isOpen="isOpenModal" @close-modal="closeModal"/>
    <div class="cart-list">
      <h2>Cart</h2>
      <h4 v-if="cart.length === 0">Your cart is empty</h4>
      <ul v-else>
        <li v-for="list in cart" :key="list.id">
          <img :src="list.img" :alt="list.name"/>
          <p>{{ list.name }}</p>
          <p>price : ${{ list.price }}</p>
          <p>quantity : {{ list.count }}</p>
          <button @click="removeCart(list.id)">X</button>
        </li>
      </ul>
    </div>
    <div class="cart-add">
      <h2>Order</h2>
      <div class="total">
        <p>Price : ${{ totalPrice }}</p>
        <p>Shipping fee : {{shippingFee===0 ? 'free':`$${shippingFee}`}}</p>
        <p>"Free shipping on orders over 40 dollars!""</p>
        <p>Total price : ${{ payment }}</p>
        <button @click="handleOpen">Purchase</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import OpenModal from './OpenModal.vue';
import { useRouter } from 'vue-router';

  const isOpenModal = ref(false);
  //라우터 인스턴스 생성
  const router = useRouter();
  const handleOpen =()=>{
    isOpenModal.value=true;
  }
  const closeModal=(value)=>{
    isOpenModal.value=value;
    emit('clear-cart',true);
    router.push('/'); //shop list 페이지로 이동
  }
  const props = defineProps({
    cart: Array
  });
  const emit = defineEmits(['remove-cart-id','clear-cart']);
  const removeCart =(cartID)=>{
    emit('remove-cart-id',cartID);
  }
  const totalPrice = computed(()=>{
    // let sum = 0;
    // // console.log(props.cart);
    // props.cart.forEach((item)=>{
    //   //가격*수량\
    //   console.log(item.price,item.count);
    //   sum += item.price * item.count;
    // });
    // return sum;

    //배열 객체 사용
    let result = props.cart.reduce((sum,item)=>{
      return  sum += item.price * item.count;
    },0);
    // console.log(result);
    return result;
  });
  const shippingFee = computed(()=>{
    return totalPrice.value >=40 ? 0:2 ;
  });
  const payment = computed(()=>{
    return totalPrice.value+shippingFee.value;
  })
</script>

<style lang="scss" scoped>
  .cart{
    display: flex;
    padding: 2rem 5rem;
    gap: 1rem;
    h4{
      color: #444;
    }
    div{
      flex: 1;
      border: 1px solid #222;
      border-radius: 5px;
    }
  }
  .cart-list{
    h2{
      background-color: antiquewhite;
      border-radius: 5px 5px 0 0;
      border-bottom: 1px solid #222;
    }
    ul{
      text-align: center;
      li{
        display: flex;
        // justify-content: space-around;
        gap: 1rem;
        align-items: center;
        padding: 1rem;
        img{
        width: 100px;
        border-radius: 5px;
        }
        button{
        cursor: pointer;
        padding: 0 5px;
        }  
      }
    }
  }
  .cart-add{
    h2{
      background-color: antiquewhite;
      border-radius: 5px 5px 0 0;
      border-bottom: 1px solid #222;
    }
    .total{
      border: none;
      padding: 1rem; 
      button{
      cursor: pointer;
      padding: 5px;
      }        
    }
  }
</style>