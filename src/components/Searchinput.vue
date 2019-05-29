<template>
            <input 
            id="search" 
            type="text" 
            name="search" 
            :class = "{margin}"
            :value="value"
            @input="handleChange"
            class="search__input"/>
</template>
<script>
export default {
    name: 'SearchInput',
    props: {
        value: {
            type: String,
            required: true,

        },
        margin:{
            type: Boolean,
            default: false
        }
    },
    methods: {
        handleChange(e){
            this.$emit('input', e.target.value);
        },
    },
}
</script>
<style lang="scss" scoped>
.search__input{
    height: 30px;

    margin-bottom: 30px;
    border: 0;
    border-bottom: 1px solid #fff;
    background: none;
    color: #fff;
    transition: all .3s ease;
    font-size: 20px;
    box-sizing: border-box;
    padding: 4px 16px;
    text-align: center;
    &:focus{
        outline: none;
        
    }

}
.margin{

        margin-top: 200px;
}
</style>

