<template>
    <h2>{{ customTitle }}</h2>
    <p>{{counter}} <sup>2</sup> = {{ squareCounter }}</p>
    <p data-testid="counter">{{ counter }}</p>
    
    <div>
        <button @click="increase">+1</button>
        <button @click="decrease">-1</button>l
    </div>


</template>

<script>
export default {
    props: {
        title: String,
        start: {
            type: Number,
            default: 100,
            //requeried: true
            validator( value ){
                return value >= 0
            }
        }
    },

    data(){
        return {
            counter: this.start
        }
    },
    methods: {
        getSquareValue(){
            return this.counter * this.counter
        },
        //increase
        increase(){
            this.counter++
        },
        //decrease
        decrease(){
            this.counter--
        }
    },
    computed: {
        squareCounter() {
            return this.counter * this.counter
        },
        customTitle() {
            //Forma más corta de hacerlo con un operador ternario 
            //return this.title ? this.title : 'Counter'

            // Otra forma de hacerlo
            return this.title || 'Counter'
            
            // Forma de hacerlo con un if
            /*if (this.title !== undefined ) {
                return this.title
            }else{
                return 'Counter'
            }*/
            
        }
    
    }
}
</script>

<style>
    button {
        background-color: #64B687;
        border-radius: 5px;
        border: 1px solid white;
        color: white;
        cursor: pointer;
        margin: 0 5px;
        padding: 5px 15px;
        transition: 0.3s ease-in-out;
    }
    button:hover {
        background-color: #5aa67b;
        transition: 0.3s ease-in-out;
    }
</style>