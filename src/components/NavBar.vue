<template>
  <nav>
    <h1>"Have fun meal!"</h1>
    <div class="router-link">
      <router-link to="/" @click="selectedClick(list)">Shop-list</router-link>
      <router-link to="/cart">Cart</router-link>
    </div>
    <ul>
      <li @click="selectedClick(list)" v-for="(list,idx) in categories" :key="idx">
        {{ list }}
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { useRouter } from 'vue-router';

  defineProps({
    categories: Array
  });
  const router = useRouter();
  const emit = defineEmits(['selected']);
  const selectedClick=(list)=>{
    emit('selected',list);
    router.push('/');
  }
</script>

<style lang="scss" scoped>
  nav{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 2rem 5rem;
    @media screen and (max-width:768px) {
      display: flex;
      flex-direction: column;
      // justify-content: center;
    }
    @media screen and (max-width:500px) {
      display: flex;
      flex-direction: column;
      // justify-content: center;
    }
    .router-link{
      display: flex;
      gap: 10px;
      margin: 10px 0;
      a{
        text-decoration: none;
        color: inherit;
        background-color: blanchedalmond;
        padding: 10px 20px;
        border-radius: 5px;
        &:hover{
        background-color: rgb(71, 71, 136);
        color: #fff;
        }
      }
    }
    ul{
      display: flex;
      background-color: antiquewhite;
      padding: 1rem;
      border-radius: 5px;
      li{
        cursor: pointer;
        padding: 5px 10px;  
        &:hover{
          color: red;
          font-weight: bolder;
        }
      }
    }
  }
</style>