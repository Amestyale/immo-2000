
<template>
    <div class="carousel">
        <button class="carousel__button carousel__button--left" @click="previous()"> 
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M224 480c-8.188 0-16.38-3.125-22.62-9.375l-192-192c-12.5-12.5-12.5-32.75 0-45.25l192-192c12.5-12.5 32.75-12.5 45.25 0s12.5 32.75 0 45.25L77.25 256l169.4 169.4c12.5 12.5 12.5 32.75 0 45.25C240.4 476.9 232.2 480 224 480z"/></svg>    
        </button>
        <img :src="image">
        <button class="carousel__button carousel__button--right" @click="next()"> 
            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 320 512"><!--! Font Awesome Pro 6.1.1 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M96 480c-8.188 0-16.38-3.125-22.62-9.375c-12.5-12.5-12.5-32.75 0-45.25L242.8 256L73.38 86.63c-12.5-12.5-12.5-32.75 0-45.25s32.75-12.5 45.25 0l192 192c12.5 12.5 12.5 32.75 0 45.25l-192 192C112.4 476.9 104.2 480 96 480z"/></svg>
        </button>
    </div>
</template>

<script>
    export default {
        props : {
            images:{
                type: Array,
                required: true,
            },
        },
        data() {
            return {
                current: 0
            }
        },
        computed: {
            image: function(){
                return this.images[this.current]
            }
        },
        methods: {
            next: function(){
                this.current = (this.current + 1 >= this.images.length ) ? 0 : this.current + 1
            },
            previous: function(){
                this.current = (this.current - 1 < 0 ) ? this.images.length - 1 : this.current - 1
            }
        }
    }
</script>

<style>
    .carousel{
        position: relative;
        height: 100%;
    }
    .carousel img{
        height: 100%;
        width: 100%;
        object-fit: cover;
    }
    .carousel__button{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        background-color: rgba(114, 18, 114, 0.5);
        border: none;
        padding: 1em;
        cursor: pointer;
    }
    .carousel__button--left{
        left: 0;
        border-radius: 0em 3em 3em 0em;
    }
    .carousel__button--right{
        right: 0;
        border-radius: 3em 0em 0em 3em;
    }
    .carousel__button svg{
        width: 1em;
        fill: white;
    }
</style>