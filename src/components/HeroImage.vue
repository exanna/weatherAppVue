<template>
   <div class="heroWrapper"></div>
</template>

<script>
   export default { name: 'HeroImage' };
</script>

<style lang="scss" scoped>

   .heroWrapper {
      position: absolute;
      top: 0;
      left: 0;
      bottom: 0;
      right: 0;
      background-image: url('../assets/bgc.jpg');
      background-repeat: no-repeat;
      background-size: cover;
      background-position: center;

      &:after {
         content: '';
         display: block;
         position: absolute;
         top: 0;
         left: 0;
         right: 0;
         bottom: 0;
         background-color: #000;
         opacity: 10%;
      }
   }
</style>