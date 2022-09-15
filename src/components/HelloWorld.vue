<script setup>
import { ref } from 'vue'

defineProps({
  msg: String
})

const m = new Map();

m.set(0, "A");
m.set(1, "A#");
m.set(2, "B");
m.set(3, "C");
m.set(4, "C#");
m.set(5, "D");
m.set(6, "D#");
m.set(7, "E");
m.set(8, "F");
m.set(9, "F#");
m.set(10, "G");
m.set(11, "G#");

// console.log(m.values())
// console.log(m.keys())


const sc = ref(""); //acorde entry


function semitono() {
  //para el input con varios acordes deberia hacer un doble for . uno para recorrer el arreglo de acordes y mas profundamente comparar con la key del map

 for (let i = 0; i < m.size; i++) {
      const el = m.get(i);
      if (el === sc.value)       counter.value = i;
     }
     }

  // for (let k = 0; k < chordArray.value.length; k++) {
  //   const element = chordArray.value[k];
  //   console.log(element)
  //   console.log("gol")
    
  


const c = ref(0); //llega a numeros infinitos, es el cobtador de semitonos. Revisar
const counter = ref(0); //es el transformador de semitonos



function increase() {
  counter.value++;
  if (counter.value > 11) {
    counter.value = 0
  }
  c.value++;
  // if (c.value>12) {
  //   c.value = 12
  // }
}

function decrement() {
  counter.value--;
  if (0 > counter.value) {
    counter.value = 11
  }
  c.value--;
  // if (c.value < -12) {
  //   c.value = -12
  // }
}

//armar un array para acordes input 

const chordArray = ref([]);

// function add() {

//   sc.value ? chordArray.value.push(sc.value) : "";
//   sc.value = "";
// }

const finalArray = ref([]);

function acordesFinal() {
  sc.value ? finalArray.value.push(m.get(counter.value)) : "";
  sc.value = "";
  c.value = 0;
}

function reset() {
  sc.value = ""
  c.value = 0;
  finalArray.value = []
  chordArray.value = []
}

</script>


<template>

  <!-- <div class="absolute -z-10 opacity-60 bg-blue-500">
    <img src="../assets/images/circle.svg" alt="" class="invert ">
    <img src="../assets/images/circle.svg" alt="" class="invert ">
    <img src="../assets/images/black.svg" alt="" class="invert "> <img src="../assets/images/black2.svg" alt=""
      class="invert">
  </div> -->


  <!-- arreglar cuando cambia el acorde se rompe con los botones del semitono -->
  <!-- agregar un aviso o instruccion para los bottones.  -->
  <h1 class="text-4xl p-2 m-2  text-blue-900 ">{{ msg }}</h1>

  <div class="p-2 m-2 text-slate-900">

    <div class="p-5">
      <h3 class="text-md">Ingresa el acorde que deseas cambiar:</h3>

      <input type="text" v-model="sc"
        class="p-1 outline-none border-b-2 border-l-2 border-rose-500 my-5 focus:bg-rose-500/10 rounded-md ">

      <!-- <button @click="add">Agregar</button>
      <div>{{chordArray}}</div> -->

      <p v-show="sc">Pulse "Listo" si este es su acorde elegido:</p>

      <div class="chord p-2 text-lg text-blue-900 font-bold">{{sc.toUpperCase()}}</div>
      <button @click="semitono"
        class="text-sm  bg-gradient-to-tr from-rose-500 to-blue-500 rounded-xl px-2 py-1 text-slate-200 hover:scale-105  hover:shadow-inner hover:shadow-rose-900 duration-500">Listo</button>
    </div>


    <div class="flex justify-between flex-shrink-0">
      <button @click="decrement"
        class="text-lg border-[0.1rem] bg-gradient-to-tr from-rose-500 to-blue-500 rounded-xl text-slate-200 px-2 py-1 m-5 focus:scale-90 hover:bg-gradient-to-tb hover:from-blue-900 hover:to-blue-300 hover:scale-110 duration-500">-1</button>
      <p v-show="sc" class="px-4 text-3xl m-5 text-blue-900">{{m.get(counter)}}</p>
      <button @click="increase"
        class="text-lg border-[0.1rem]  bg-gradient-to-tr from-rose-500 to-blue-500 rounded-xl px-2 py-1  m-5 text-slate-200 focus:scale-90 hover:bg-gradient-to-tb hover:from-blue-900 hover:to-blue-300 hover:scale-110 duration-500">+1</button>
    </div>


    <p class="m-4 text-xs">Transposición: {{c}}</p>


    <button @click="acordesFinal"
      class="text-sm border-[0.1rem] bg-gradient-to-tr from-rose-500 to-blue-500 rounded-xl px-2 py-1 mx-5 my-2 text-slate-200 hover:scale-105  hover:shadow-inner hover:shadow-rose-900 duration-500">Guardar
      acordes</button>


    <h4 v-show="finalArray!=''" class="mt-4">Los acordes de tu canción:</h4>

    <div v-show="finalArray!=''"
      class="flex justify-center items-centers border-blue-900 border-[0.1rem] m-2 rounded-xl flex-wrap max-w-4">
      <div v-for="a,index in finalArray" :key="index" class="text-xl">
        <div class="p-2 text-blue-900">{{a}}</div>
      </div>
    </div>



    <button type="reset" @click="reset"
      class="text-xs border-[0.1rem]  bg-gradient-to-tr from-rose-500 to-blue-500 rounded-xl px-2 py-1 mx-5 my-2 text-slate-200 hover:scale-105  hover:shadow-inner hover:shadow-rose-900 duration-500">Reiniciar</button>


  </div>

</template>

<style scoped>
h1 {
  font-family: 'Anton', sans-serif;
}

button {
  font-family: 'Poppins', sans-serif;
}

p {
  font-family: 'Poppins', sans-serif;
}

h3 {
  font-family: 'Poppins', sans-serif;

}

h4 {
  font-family: 'Poppins', sans-serif;

}

.chord {
  font-family: 'Poppins', sans-serif;


}
</style>
