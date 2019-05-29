<template>
    <div :class="[{bgChange: step === 1} , 'app']">
        <transition name="slide">
        <img src="./assets/logo.png" alt="Logo" class="logo" v-if="step === 1"/>
        </transition>
        <transition name="fade">
        <BackgroundImage  v-if="step === 0"/>
        </transition>
        
        <Claim v-if="step === 0" />
        <SearchInput v-model="searchValue" @input="handleInput" :margin="step === 1"/>
       
        <div class="results" v-if="results && !loading && step === 1">
            <Item 
            v-for="item in results"
            :item="item" 
            :key="item.data[0].nasa_id"
            @click.native="handleModalOpen(item)"
            />
        </div>
        <div v-if="step === 1 && loading" class="loader"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
        <Modal 
        v-if="modalOpen" 
        @closeModal="modalOpen = false"
        :item="modalItem"
        />
    </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/Searchinput.vue';
import BackgroundImage from '@/components/BackgroundImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = "https://images-api.nasa.gov/search";

export default {
    name: 'App',
    components: { Claim, SearchInput, BackgroundImage, Item, Modal},
    data(){
        return{
            modalOpen: false,
            modalItem: null,
            searchValue: '',
            results: [],
            loading: false,
            step: 0,
        }
    },
    methods:{
        handleModalOpen(item){
            this.modalOpen = true;
            this.modalItem = item;
        },
        // eslint-disable-next-line
        handleInput: debounce(function(){
            this.loading = true;
            axios.get(`${API}?q=${this.searchValue}&media_type=image`)
            .then((response)=>{
            this.results = response.data.collection.items
              this.loading = false;
              this.step = 1;
            })
            .catch((error) => {
                console.log(error);
                
            });
        }, 500)
    }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

*{
  box-sizing: border-box;
   -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body{
  font-family: 'Monsterrat', sans-serif;
  margin: 0;
}

.fade-enter-active, .fade-leave-active{
transition: opacity .3s ease;
}

.fade-enter, .fade-leave-to{
opacity: 0;
}

.slide-enter-active, .slide-leave-active{
transition: margin-top .3s ease;
}

.slide-enter, .slide-leave-to{
margin-top: -50px
}

.app{
    position: relative;
    display: flex;
    flex-flow: column nowrap;
    align-items: center;
    margin: 0;
   justify-content: flex-start;
    width: 100%;
    min-height: 100vh; 
  
}

.logo{
    position: absolute;
    top: 0px;
    width: 320px;
    height: 200px;
}


.results{
    width: 100%;
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 20px;
    margin-top: 20px;
    box-sizing: border-box;
    padding: 0 20px;
     @media only screen and (min-width: 768px) {
           grid-template-columns: 1fr 1fr;
        }
           @media only screen and (min-width: 1200px) {
           grid-template-columns: 1fr 1fr 1fr;
        }
}
.bgChange{
    background: url('http://www.script-tutorials.com/demos/360/images/stars.png'), linear-gradient(to right, #0A2342, #551f2f);
}
.loader {
  display: inline-block;
  position: relative;
  width: 64px;
  height: 64px;
}
.loader div {
  animation: loader 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  transform-origin: 32px 32px;
}
.loader div:after {
  content: " ";
  display: block;
  position: absolute;
  width: 6px;
  height: 6px;
  border-radius: 50%;
    background-image: linear-gradient(to right top, #051937, #004d7a, #008793, #00bf72, #a8eb12);
  margin: -3px 0 0 -3px;
}
.loader div:nth-child(1) {
  animation-delay: -0.036s;
}
.loader div:nth-child(1):after {
  top: 50px;
  left: 50px;
}
.loader div:nth-child(2) {
  animation-delay: -0.072s;
}
.loader div:nth-child(2):after {
  top: 54px;
  left: 45px;
}
.loader div:nth-child(3) {
  animation-delay: -0.108s;
}
.loader div:nth-child(3):after {
  top: 57px;
  left: 39px;
}
.loader div:nth-child(4) {
  animation-delay: -0.144s;
}
.loader div:nth-child(4):after {
  top: 58px;
  left: 32px;
}
.loader div:nth-child(5) {
  animation-delay: -0.18s;
}
.loader div:nth-child(5):after {
  top: 57px;
  left: 25px;
}
.loader div:nth-child(6) {
  animation-delay: -0.216s;
}
.loader div:nth-child(6):after {
  top: 54px;
  left: 19px;
}
.loader div:nth-child(7) {
  animation-delay: -0.252s;
}
.loader div:nth-child(7):after {
  top: 50px;
  left: 14px;
}
.loader div:nth-child(8) {
  animation-delay: -0.288s;
}
.loader div:nth-child(8):after {
  top: 45px;
  left: 10px;
}
@keyframes loader {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
