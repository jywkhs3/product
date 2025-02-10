<template>
  <nav>
    <h1>Have fun meal!</h1>
    <ul>
      <li @click="selectedClick(list)" v-for="(list,idx) in categories" :key="idx">
        {{ list }}
      </li>
    </ul>
  </nav>
</template>

<script setup>
  defineProps({
    categories: Array
  });
  const emit = defineEmits(['selected']);
  const selectedClick=(list)=>{
    emit('selected',list);
  }
</script>

<style lang="scss" scoped>
  nav{
    display: flex;
    justify-content: space-between;
    padding: 2rem 5rem;
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