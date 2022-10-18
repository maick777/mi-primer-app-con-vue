<script setup>
//CONSTANTES

import {
    ref,
    computed
} from 'vue'

const name = "Vue Dinamico";
const styleColor = "color: blue";
const arrayColores = ["blue", "red", "peru"];
const activo = true;
const estado = true;
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"]

const arrayVerduras = [{
        id: 1,
        name: "Tomate",
        price: "$5.00",
        img: "🍅",
        description: "Es un tomate roja madura"
    },
    {
        id: 2,
        name: "Coliflor",
        price: "$5.00",
        img: "🥦",
        description: "Es una Coliflor verde"
    },
    {
        id: 3,
        name: "Zanahoria",
        price: "$5.00",
        img: "🥕",
        description: "Es una nahahoria para mi conejo"
    }

]

const objetoCarro = {

    id: 1,
    name: "Toyota",
    price: "$50000.00",
    img: "🚗",
    description: "Es una carrito Toyota"
}

const arrayPersonas = [{
        id: 1,
        name: "Maria",
        edad: 35,
        sexo: 2
    },
    {
        id: 2,
        name: "José",
        edad: 25,
        sexo: 1
    },
    {
        id: 3,
        name: "Jorge",
        edad: 15,
        sexo: 1
    }

]

let counter = ref(0)
let arrayFavoritos = ref([]);

const increment = () => counter.value++
const disminuir = () => counter.value--
const resetear = () => (counter.value = 0)

//MÉTODOS

const hanndleClick = () => {
    console.log('Me diste Click')

}

const hanndleClick2 = (message) => {
    console.log(message + ' Obtenido')
}

//PROPIEDADES COMPUTADAS (Siempre con return)
const classCouter = computed(() => {
    if (counter.value === 0) {
        return 'zero'
    }
    if (counter.value > 0) {
        return 'positive'
    }
    if (counter.value < 0) {
        return 'negative'
    }
})

const add = () => {
    arrayFavoritos.value.push(counter.value)
}

const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find((num) => num === counter.value)
    //if(numSearch === 0) return true
    //return numSearch ? true : false
    return numSearch || numSearch === 0

})
</script>

<template>
<div class="container m3">

    <span>1.- CAPTURAR NOMBRE:</span>
    <h2>{{ name }}</h2>

    <span>2.- COMVERTIR TODO A MAYÚSCULA:</span>
    <h2>{{ name.toUpperCase() }}</h2>

    <span>3.- SELECCIONAR COLOR DE UN ARRAY</span>
    <h2 :style="`color: ${arrayColores[0]}`">{{ arrayColores[0] }} </h2>

    <span>4.- IF - ELSE</span>
    <p v-if="activo">Activo</p>
    <p v-else>Inactivo</p>

    <span>5.- IF - ELSEIF - ELSE</span>
    <p v-if="estado === true">Pagado</p>
    <p v-else-if="estado === false">Pendiente</p>
    <p v-else>Sin estado</p>

    <span>6.- V-SHOW (Mostrar y ocultar cuando sea necesario)</span>
    <h3 v-show="activo">Visible -True</h3>

    <span>7.- V-FOR (of/in) (Array de string)</span>
    <ul>
        <li v-for="(fruta, index) of arrayFrutas" :key="index">
            {{index}} - {{ fruta }}
        </li>
    </ul>

    <span>8.- TAREA DE ARRAY (v-for) (Array de objetos)</span>
    <ul>
        <li v-for="verdura in arrayVerduras" :key="verdura.id">
            {{verdura.id}} {{verdura.img}} - {{verdura.name}} - {{verdura.price}} - {{verdura.description}}
        </li>
    </ul>

    <span>9.- OBJETOS </span>
    <ul>
        <li v-for="(value, propiedad, index) in objetoCarro" :key="index">
            {{index}}-{{propiedad}}: {{value}}
        </li>
    </ul>

    <span>10.- V-IF DENTRO DE V-FOR</span>
    <ul class="list-group mt-2">
        <li class="list-group-item" v-for="item in arrayPersonas" :key="item.id">
            <i v-if="item.sexo == 1">Masculino</i>
            <i v-else>Femenino</i>
            {{item.name}} - {{item.edad}}
        </li>
    </ul>
    <ul class="list-group mt-2">
        <template v-for="item in arrayPersonas" :key="item.id">
            <li class="list-group-item" v-if="item.edad > 20">
                {{item.name}} - {{item.edad}}
            </li>
        </template>
    </ul> <br>

    <span>11.- EVENTOS (Ver resultado en consola)</span> <br>
    <div class="btn-group">
        <button v-on:click="hanndleClick2('5')" class="btn btn-success">Click (Con parámetro)</button>
        <button @click="hanndleClick" class="btn btn-primary">Click</button> <br>
    </div> <br> <br>

    <span>12.- REACTIVIDAD - ref(): (Contador) </span>

    <h2 :class="counter > 0 ? 'positive': 'negative' "> {{counter}} </h2>

    <span>Con Computed</span>
    <h2 :class="classCouter"> {{counter}} </h2>

    <div class="btn-group">

        <button @click="increment" class="btn btn-success">Incrementar</button>
        <button @click="disminuir" class="btn btn-danger">Disminuir</button>
        <button @click="resetear" class="btn btn-info">Reset</button>
        <button @click="add" class="btn btn-primary" :disabled="bloquearBtnAdd">Add</button>
    </div> <br>

    <span>COMPUTADAS (Ejercicio)</span>

    <ul class="list-group mt-2">
        <li class="list-group-item" v-for="(num,index) in arrayFavoritos" :key="index">
            {{num}}
        </li>

    </ul>

</div>
</template>

<style scoped>
span {
    color: red;
}

.positive {
    color: #606bff
}

.negative {
    color: red;
}

.zero {
    color: orange;
}
</style>
