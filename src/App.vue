<script setup>
import { ref } from 'vue'
const mostrarDiv = ref(false)


const produtos = ref([
  {
    id: 1,
    nome: 'Biblioteca da Meia noite',
    preco: 34.90,
    quant: 1,
    img: "l1.jpg"
  },
  {
    id: 2,
    nome: 'É assim que começa (Vol. 2 É assim que acaba)',
    preco: 31.0,
    quant: 1,
    img: "l2.jpg"
  },
  {
    id: 3,
    nome: 'É Assim que Acaba: 1 ',
    preco: 33.0,
    quant: 1,
    img: 'l3.jpg'
  },
  {
    id: 4,
    nome: 'Tudo é rio',
    preco: 37.9,
    quant: 1,
    img: 'l4.jpg'
  },
  {
    id: 5,
    nome: 'Mulheres que correm com os lobos',
    preco: 38.9,
    quant: 1,
    img: 'l5.jpg'
  },
  {
    id: 6,
    nome: 'The Sherlock Holmes',
    preco: 100,
    quant: 1,
    img: 'l6.jpg'
  },
  {
    id: 7,
    nome: 'A mandíbula de Caim',
    preco: 37.8,
    quant: 1,
    img: 'l7.jpg'
  },
  {
    id: 8,
    nome: 'Os sete maridos de Evelyn Hugo',
    preco: 31.9,
    quant: 1,
    img: 'l8.jpg'
  },
  {
    id: 9,
    nome: 'Daisy Jones and The Six',
    preco: 32.9,
    quant: 1,
    img: 'l9.jpg'
  },
  {
    id: 10,
    nome: 'A vida invisível de Addie LaRue',
    preco: 45.4,
    quant: 1,
    img: 'l01.jpg'
  },
  {
    id: 11,
    nome: 'Pinóquio',
    preco: 47.9,
    quant: 1,
    img: 'l02.jpg'
  },
  {
    id: 12,
    nome: 'O colecionador ',
    preco: 46.0,
    quant: 1,
    img: 'l04.jpg'
  },
])


const carrinho = ref({
  items: [],
  valorTotal: 0,
})


function addliv(pos) {
  produtos.value[pos].quant++
}
function removerliv(pos) {
  if (produtos.value[pos].quant > 1) {
    produtos.value[pos].quant--
  }
}
function addCarrinho(i) {
  const produto = produtos.value[i]
  carrinho.value.items.push({ ...produto, total: produto.preco * produto.quant })
  carrinho.value.valorTotal += produto.preco * produto.quant
}
function removerCarrinho(i) {
  carrinho.value.items.splice(i, 1)
  totalCarrinho()
}


function totalCarrinho() {
  carrinho.value.valorTotal = 0
  for (let item of carrinho.value.items) {
    carrinho.value.valorTotal += item.quant * item.preco
  }
}
</script>


<template>
  <fieldset>
    <h1>Livraria ON-LINE</h1>
  </fieldset>
  <p></p>
  <h3 class="subh2">Os livros preferidos do momento: </h3>
  <p></p>
  <div class="produtos">
    <div v-for="(produto, i) in produtos" :key="i" class="card-produto">
      <img :src="produto.img">
      <h2>{{ produto.nome }}</h2>
      <p> R$ {{ produto.preco.toFixed(2).replace('.', ',') }}</p>
      <p> Quantidade: {{ produto.quant }}</p>
      <div class="botoes">
        <button @click="addliv(i)">+</button>
        <button @click="removerliv(i)">-</button>
        <button @click="addCarrinho(i)" class="addCarrinho">Adicionar ao carrinho</button>
      </div>
    </div>
  </div>
  <li>
    <button @click="mostrarDiv = !mostrarDiv" class="btncard"> Ver carrinho</button>
  </li>
  <div class="card" v-if="(mostrarDiv = mostrarDiv)">
    <h2>carrinho</h2>
    <ul>
      <li v-for="(item, i) in carrinho.items" :key="item.id">
        Quantidade: {{ item.quant }}
        <p>Produto: {{ item.nome }}: R${{ item.preco }}</p>
        <button @click="removerCarrinho(i)">remover</button>
      </li>
      <button @click="mostrarDiv = !mostrarDiv">Continuar comprando</button>
    </ul>
    Valor total a pagar: R${{ carrinho.valorTotal.toFixed(2) }}
  </div>
</template>

<style scoped>
fieldset {
  border-radius: 8px;
}
h1 {
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}.subh2 {
  text-align: center;
  color: black;
}.btncard {
  border: none;
  padding: 10px;
  background-color: rgb(229, 221, 211);
  font-family: Arial, Helvetica, sans-serif;
  margin-left: 45rem;
  font-size: 15px
}
.card {
  border: none;
  margin-bottom: 1rem;
  padding: 15px;
  width: 350px;
  height: 100px;
  margin-left: 40rem;

}
.card-produto img {
  margin-top: 20px;
  width: 70%;
}
.card-produto {
  margin-right: 2rem;
  width: 299px;
  height: 480px;
  border-radius: 8px;
  box-shadow: rgba(117, 65, 65, 0.35) 0px 5px 15px;
  display: flex;
  flex-direction: column;
  align-items: center;


}
.card-produto:hover {
  width: 300px;
  height: 480px;
  border-radius: 5px;
  box-shadow: rgba(117, 65, 65, 0.35) 0px 5px 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgba(175, 161, 143, 0.226);

}
.produtos {
  margin: 200px;
  margin-top: 30px;
  margin-left: 10%;
  display: grid;
  grid-template-columns: repeat(4, 10fr);
  grid-auto-rows: 40%;
}
h2,
p {
  margin: 4px;
  color: rgb(78, 78, 78);
  font-family: Arial, Helvetica, sans-serif;
  font-size: 14px;
  color: black;
}
button {
  background-color: rgb(207, 199, 199);
  border-radius: 4px;
  border: none;
  font-family: Arial, Helvetica, sans-serif;
  margin: 2px;
  font-size: 15px;
}
button:hover {
  background-color: rgb(230, 227, 227);
}
</style> 
