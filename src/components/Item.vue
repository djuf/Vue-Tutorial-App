<template>
        <div :style="style" class="item">
       </div>
</template>
<script>
export default {
    name: 'Item',
    props:{
    item: {
        type: Object,
        required: true,
    },
    },
    data(){
        return{
            photo: '',
            title: this.item.links[0].title,
            style:{}
        }
    },
    mounted(){
        this.photo = this.item.links[0].href;
        this.style = {
            backgroundImage: `url("${this.photo}")`
        }
    }
}
</script>
<style lang="scss" scoped>
.item{
  
    height: 300px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;
}
</style>
