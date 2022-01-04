<template>
<img v-if="img" :src="img" alt="bg"> <!-- utilizamos un v:bind == ':' / preguntamos con el v-if si hay una imagen-->
<div class="bg-dark"></div>

<div class="indecision-container">

    <input 
        type="text" 
        placeholder="Hazme una pregunta" 
        v-model="newQuestion">
    <p>Recuerda terminar con un signo de interrogación (?)</p>

    <div v-if="isValidPregunta">
        <h2>{{newQuestion}}</h2>
        <h1>{{answer}}</h1>
    </div>

</div>
</template>

<script>
export default {
    data() {
        return {
            newQuestion: null,
            answer: null,
            img: null,
            isValidPregunta: false
        }
    },
    methods: {
        async getAnswer() { // con este metodo realizamos nuestra petición http

            try {
                this.answer = 'Pensando...'
                const { answer, image } = await fetch('https://yesno.wtf/api').then(r => r.json())

                // mandamos a llamar los elementos que necesitamos
                this.answer = answer === 'yes' ? 'Si' : 'No!!'
                this.img = image

            } catch (error) {
                console.log('IndecisionComponent: ', error )
                this.answer = 'No se pudo cargar del API'
                this.img = null
            }

        }
    },
    watch: {
        newQuestion(value, oldValue) {

            this.isValidPregunta = false

            console.log({
                value
            }) // Nueva linea agregada ------------------------

            if (!value.includes('?')) return

            this.isValidPregunta = true

            //TODO: Realizar petición http 
            this.getAnswer(); // mandamos a traer el metodo por separado

        }
    }
}
</script>

<style scoped>
img,
.bg-dark {
    height: 100vh;
    left: 0px;
    max-height: 100%;
    max-width: 100%;
    position: fixed;
    top: 0px;
    width: 100vw;
}

.bg-dark {
    background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
    position: relative;
    z-index: 99;
}

input {
    width: 250px;
    padding: 10px 15px;
    border-radius: 5px;
    border: none;
}

input:focus {
    outline: none;
}

p {
    color: white;
    font-size: 20px;
    margin-top: 0px;
}

h1,
h2 {
    color: white;
}

h2 {
    margin-top: 150px;
}
</style>
