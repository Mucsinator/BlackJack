<script setup>
import { ref } from 'vue';

let PlayerCards = ref([])
let DealaerCards = ref([])
let cards = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10", "11", "10", "10", "10"]




function RandomKartya() {
  return Math.floor(Math.random() * (14 - 0))
}



const DealerHúzás = () => {

  DealaerCards.value.push(cards[RandomKartya()])



}




const OsszeSzamol = (lista) => {
  let OsszeSzamol = 0
  lista.forEach(item => {
    OsszeSzamol += parseInt(item)

  })
  return OsszeSzamol
}


const vizsgalat = () => {


  if (OsszeSzamol(PlayerCards.value) >= 21 && OsszeSzamol(DealaerCards.value) >= 21) {
    alert("Döntetlen!")
    PlayerCards.value = []
    DealaerCards.value = []
    return
  }

  if (OsszeSzamol(PlayerCards.value) >= 21) {
    alert("Az Osztó Nyert!")
    PlayerCards.value = []
    DealaerCards.value = []
    return
  }

  if (OsszeSzamol(DealaerCards.value) >= 21) {
    alert("A Játékos Nyert!")
    PlayerCards.value = []
    DealaerCards.value = []
    return
  }
}


const Húzás = () => {

  vizsgalat()


  let RandomCard = cards[RandomKartya()]
  PlayerCards.value.push(RandomCard)
  DealerHúzás();
}





</script>

<template>
  <div>
    <h1>Player</h1>
    <button @click="Húzás">Draw</button>
    <ul>
      <li v-for="card in PlayerCards">{{ card }}</li>
    </ul>
  </div>

  <div>{{ OsszeSzamol(PlayerCards) }}</div>



  <div>
    <h1>Dealaer</h1>
    <ul>
      <li v-for="card in DealaerCards">{{ card }}</li>
    </ul>
  </div>

  <div>{{ OsszeSzamol(DealaerCards) }}</div>
</template>




<style scoped></style>
