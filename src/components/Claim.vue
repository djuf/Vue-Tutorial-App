<template>
<div class="claimWrapper">
    <h1 class="header">Spacer</h1>
    <p class="paragraph">
        Type anything space-related to start.
    </p>
</div>
</template>
<script>
export default {
    name: 'Claim',
}
</script>

<style lang="scss" scoped>
.claimWrapper{
    color: #fff;
    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;
    text-align: center;
      padding-top: 30px;
    box-sizing: border-box;
     @media only screen and (min-width: 768px) {
              box-sizing: border-box;
              padding: 50px 20%;
              
        }
 @media only screen and (min-width:1200px){
     color: #fff;
    padding: 20px 20%;
 }
    .header{
        font-size:50px;
        margin:0;
        font-weight: 800;
        text-transform: uppercase;
        @media only screen and (min-width: 768px) {
            font-size:80px;
        }
}
.paragraph{
    margin: 20px 0 0 0;
    font-size: 15px;
    font-weight: 600;
      @media only screen and (min-width: 768px) {
            font-size:20px;
        }
}
}

</style>
