<script setup>
import { reactive } from 'vue';

const nome = 'gian'
const meuObj = {
  nome: 'gian',
  filmeFavorito: 'Rocky'
}

function dizOla(nome) {
  return `${nome} diz oi`;
}

const enderecoDaImageDoBatman = 'https://recreio.uol.com.br/media/uploads/dc_comics/batman_cavaleiro_das_trevas_capa.jpg'
const enderecoDaImageDoSuperman = 'https://www.donanimhaber.com/cache-v2/?t=20230417154444&width=-1&text=0&path=https://www.donanimhaber.com/images/images/haber/158117/henry-cavill-superman-rolunu-birakti-yeni-filmler-yolda158117_1.jpg'

const botaoEstaDesabilitado = false

const gostaDoBatman = false
const gostaDoSuperman = false

const estaAutorizado = true


// let contador = 0;
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferindo: 0,
  nomes: ['gian', 'paulo', 'luisa', 'monica'],
  nomeAInserir: '',
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

// function mostraSaldoFuturo() {
//   return estado.saldo - estado.transferindo
// }
// é o mesmo que 

function mostraSaldoFuturo() {
  const {saldo, transferindo} = estado;
  return saldo - transferindo;
}

function validaValorTransferencia() {
  const {saldo, transferindo} = estado;
  return saldo >= transferindo;
}

function cadastrarNome() {
  if(estado.nomeAInserir.length >= 3){
    estado.nomes.push(estado.nomeAInserir)
  } else {
    alert('Digite mais caracteres')
  }
}



</script>

<template>
  <h1>{{ dizOla('Paula') }}</h1>
  <img v-if="gostaDoBatman" :src="enderecoDaImageDoBatman" alt="">
  <img v-else-if="gostaDoSuperman" :src="enderecoDaImageDoSuperman" alt="">
  <h2 v-else>Não curte heróis da DC</h2>

  <h1 v-if="estaAutorizado">Bem-vindo</h1>
  <h1 v-else>Não possui acesso</h1>

  <button :disabled="botaoEstaDesabilitado">enviar mensagem</button>

  <br>
  <hr>

  {{ estado.contador }}

  <button @click="incrementar" type="button">+</button>
  <button @click="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }} <br>
  Transferindo: {{ estado.transferindo }} <br>
  Saldo depois da transferência: {{ mostraSaldoFuturo() }} <br>
  <input class="campo" :class="{ invalido: !validaValorTransferencia()}" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br />
  <hr />

  <ul>
    <li v-for="nome in estado.nomes">
      {{ nome }}
    </li>
  </ul>
  <input @keyup="evento => estado.nomeAInserir = evento.target.value" type="text"  placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nomes</button>

  <h3 v-for="nome in estados.nomes">{{ nome }}</h3>
</template>

<style scoped>

img {
  max-width: 200px;
}

.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid black;
}

</style>
