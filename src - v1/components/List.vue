<template>
  <div class="product-list">
    <div class="card" v-for="list in products" :key="list.id">
      <img :src="list.img" :alt="list.name"/>
      <p>price : ${{ list.price }}</p>
      <button @click="addToList(list)">add to cart</button>
    </div>
  </div>
</template>

<script setup>
  defineProps({
    products : Array
  });
  const emit = defineEmits(['add-to-cart']);
  const addToList=(list)=>{
    emit('add-to-cart',list);
  }
</script>

<style lang="scss" scoped>
  .product-list{
    display: flex;
    justify-content: center;
    gap: 2rem;
  }
  .card{
    width: 200px;
    text-align: center;
    img{
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 5px;
    }
  }
</style>