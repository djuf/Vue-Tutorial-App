<template>
    <div class="backgroundImage" />
</template>
<script>
export default {
    name:"BackgroundImage",
};
</script>
<style lang="scss" scoped>
.backgroundImage{
    height: 100vh;
    width: 100%;
    filter: saturate(1.25);
    background: url('../assets/heroimage.jpg') no-repeat;
    background-size: cover;
    position: fixed;
    z-index: -1;
    background-position: 50% 0%;
         @media only screen and (min-width: 768px) {
        
        }
           @media only screen and (min-width: 1200px) {
          
        }
}
</style>
