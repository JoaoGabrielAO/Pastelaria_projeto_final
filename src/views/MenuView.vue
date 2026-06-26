<template>
  <div class="menu">
    <h1>Nosso Cardápio</h1>
    <p class="subtitulo">Escolha o seu pastel favorito 🥟</p>

    <div class="lista-pasteis">
      <div class="card" v-for="pastel in cardapio" :key="pastel.id">
        <div class="emoji">{{ pastel.emoji }}</div>
        <h3>{{ pastel.nome }}</h3>
        <p class="descricao">{{ pastel.descricao }}</p>
        <span class="preco">A partir de R$ {{ pastel.precoBase.toFixed(2) }}</span>
        <button @click="pedir(pastel)">Pedir</button>
      </div>
    </div>
  </div>
</template>

<script>
import { API_URL } from "@/api.js";

export default {
  name: "MenuView",
  data() {
    return {
      cardapio: [],
    };
  },
  mounted() {
    fetch(`${API_URL}/cardapio`)
      .then((resposta) => resposta.json())
      .then((dados) => {
        this.cardapio = dados;
      });
  },
  methods: {
    pedir(pastel) {
      this.$router.push({ name: "config", query: { sabor: pastel.nome } });
    },
  },
};
</script>

<style scoped>
.menu {
  padding: 30px;
}

.menu h1 {
  color: #7a2d10;
}

.subtitulo {
  color: #666;
  margin-bottom: 30px;
}

.lista-pasteis {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.card {
  background: #fff;
  border: 2px solid #f0a500;
  border-radius: 12px;
  padding: 20px;
  width: 240px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.emoji {
  font-size: 50px;
}

.card h3 {
  color: #7a2d10;
  margin: 10px 0;
}

.descricao {
  color: #777;
  font-size: 14px;
  min-height: 50px;
}

.preco {
  display: block;
  color: #b5451b;
  font-weight: bold;
  margin: 10px 0;
}

.card button {
  background: #7a2d10;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 15px;
}

.card button:hover {
  background: #f0a500;
  color: #3d1508;
}
</style>