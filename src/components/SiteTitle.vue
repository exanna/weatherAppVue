<template>   
   <h1 class="title">Check the weather</h1>   
</template>

<script>

export default { name: 'Title' };
</script>

<style lang="scss" scoped>

.title {
   color: white;
   z-index: 1; 
   text-align: center;
   font-size: 20px;
   font-weight: 400;
   margin-top: -160px;

   @media (min-width: 768px) {
      font-size: 40px;
   }
}
</style>