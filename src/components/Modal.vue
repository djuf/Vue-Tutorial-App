<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="photo" alt="">
            </div>
            <div class="description">
                <h2 class="title">
                    {{ title }}
                </h2>
                <p class="paragraph">
                    {{ description }}
                </p>
              
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')"></div>
    </div>
</template>

<script>
export default {
name: "Modal",
props:{
    item:{
        type: Object,
        required: true,
    }
},
data() {
    return {
        photo: null,
        title: null,
        description: null,
    }
},
mounted(){
        this.photo = this.item.links[0].href;
        this.title = this.item.data[0].title;
        this.description =  this.item.data[0].description;
}
}
</script>

<style lang='scss' scoped>
.outerWrapper{
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: url('../assets/modal.png') #f6f6f6;
   background-size: 60%;
    background-repeat: no-repeat;
        background-position: 100% 100%;
      @media only screen and (min-width: 1200px) {
          max-width: 70%;
          max-height: 55%;
          left: 15%;
          top: 22.5%;
          margin: auto;
          box-shadow: 0 30px 30px -10px rgba($color: #000000, $alpha: .3);
           background-size: 30%;
    background-position: 100% 100%;
      }
}
.innerWrapper{
    display: flex;
    height: 100%;
    padding: 50px 10px;
    justify-content: flex-start;
    align-items: center;
    flex-flow: column nowrap;
          @media only screen and (min-width: 1200px) {
              flex-flow: row nowrap;
              .photo{
    height: 100%;
    width: 50%;
    margin: 20px;
    img{
        max-height: 100%;
    }
              }
          }
}
.photo{
    max-width: 100%;
    height: auto;
    display: flex;
    justify-content: center;
    align-items: center;
}
img{
    width: 100%;
}
.description{
    color: #333;
    width: 100%;


    overflow-y: auto;
    max-height: 100%;
}
h2{
    text-align:center;
}
p{  
    margin: 0 auto;
    word-wrap: break-word;
    max-width: 80%;

}
.close{
    width: 30px;
    height: 30px;
    position: absolute;
    right: 10px;
    top: 30px;
    cursor: pointer;
      &::before,
    &::after{
         position: absolute;
        content: "";
        width: 20px;
        height: 2px;
        background: #000;
        display:block;
    }
     &::before{
         transform: rotate(45deg);
     }
      &::after{
        transform: rotate(-45deg);
      }
}
  


</style>