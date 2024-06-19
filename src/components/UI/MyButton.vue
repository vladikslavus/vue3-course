<template>
    <button class="btn"><slot></slot></button>
</template>

<script>
export default {
  name: 'my-button'
};
</script>

<style scoped>
.btn {  
  padding: 10px 15px;
  color: teal;
  font-weight: 900;
  background: none;
  cursor: pointer;
  border: 1px solid teal;
}
</style>
