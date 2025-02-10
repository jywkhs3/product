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
    .router-link{
      flex: 1;
      display: flex;
      gap: 10px;
      margin: 10px;
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
      padding: 1rem 1.5rem;
      border-radius: 5px;
      gap: 2rem;
      li{
        cursor: pointer;  
        &:hover{
          color: red;
          font-weight: bolder;
        }
      }
    }
  }
</style>