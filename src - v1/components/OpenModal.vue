<template>
  <div class="modal-overlay" v-if="isOpen">
    <div class="modal">
      <h2>Complete!</h2>
      <p>Your order has been successfully completed.</p>
      <button @click="handleClose">done</button>
    </div>
  </div>
</template>

<script setup>
  defineProps({
    isOpen: Boolean //true,false
  });
  const emit = defineEmits(['close-modal']);
  const handleClose=()=>{
    emit('close-modal',false);
  }
</script>

<style lang="scss" scoped>
  .modal-overlay{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    .modal{
      background-color: #fff;
      padding: 3rem 5rem;
      button{
        cursor: pointer;
      }
    }
  }
</style>