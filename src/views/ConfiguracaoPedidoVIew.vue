<template>
  <div class="config">
    <h1>Monte seu Pedido</h1>

    <AlertaComponent
      :visivel="alerta.visivel"
      :tipo="alerta.tipo"
      :mensagem="alerta.mensagem"
    />

    <div class="formulario">
      <label>Nome do Cliente *</label>
      <input type="text" v-model="pedido.cliente" placeholder="Digite seu nome" />

      <label>Sabor do Pastel *</label>
      <select v-model="pedido.sabor">
        <option value="">Selecione um sabor</option>
        <option v-for="p in cardapio" :key="p.id" :value="p.nome">
          {{ p.nome }}
        </option>
      </select>

      <label>Tamanho *</label>
      <select v-model="pedido.tamanho">
        <option value="">Selecione um tamanho</option>
        <option v-for="t in tamanhos" :key="t.id" :value="t.nome">
          {{ t.nome }}
        </option>
      </select>

      <label>Opcionais</label>
      <div class="opcionais">
        <label v-for="o in opcionais" :key="o.id" class="checkbox">
          <input type="checkbox" :value="o.nome" v-model="pedido.opcionais" />
          {{ o.nome }}
        </label>
      </div>

      <button class="btn-confirmar" @click="confirmarPedido">
        Confirmar Pedido
      </button>
    </div>
  </div>
</template>

<script>
import AlertaComponent from "@/components/AlertaComponent.vue";
import { API_URL } from "@/api.js";

export default {
  name: "ConfiguracaoPedidoView",
  components: {
    AlertaComponent,
  },
  data() {
    return {
      cardapio: [],
      tamanhos: [],
      opcionais: [],
      pedido: {
        cliente: "",
        sabor: "",
        tamanho: "",
        opcionais: [],
      },
      alerta: {
        visivel: false,
        tipo: "info",
        mensagem: "",
      },
    };
  },
  mounted() {
    fetch(`${API_URL}/cardapio`)
      .then((r) => r.json())
      .then((dados) => (this.cardapio = dados));

    fetch(`${API_URL}/tamanhos`)
      .then((r) => r.json())
      .then((dados) => (this.tamanhos = dados));

    fetch(`${API_URL}/opcionais`)
      .then((r) => r.json())
      .then((dados) => (this.opcionais = dados));

    if (this.$route.query.sabor) {
      this.pedido.sabor = this.$route.query.sabor;
    }
  },
  methods: {
    mostrarAlerta(tipo, mensagem) {
      this.alerta.tipo = tipo;
      this.alerta.mensagem = mensagem;
      this.alerta.visivel = true;
    },
    confirmarPedido() {
      if (!this.pedido.cliente) {
        this.mostrarAlerta("erro", "Por favor, informe o nome do cliente.");
        return;
      }
      if (!this.pedido.sabor) {
        this.mostrarAlerta("erro", "Escolha o sabor do pastel.");
        return;
      }
      if (!this.pedido.tamanho) {
        this.mostrarAlerta("aviso", "Selecione o tamanho do pastel.");
        return;
      }

      fetch(`${API_URL}/pedidos`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(this.pedido),
      })
        .then((r) => r.json())
        .then(() => {
          this.mostrarAlerta("sucesso", "Pedido confirmado com sucesso!");
          setTimeout(() => {
            this.$router.push({ name: "pedidos" });
          }, 1500);
        });
    },
  },
};
</script>

<style scoped>
.config {
  padding: 30px;
  max-width: 500px;
  margin: 0 auto;
  text-align: left;
}

.config h1 {
  color: #7a2d10;
  text-align: center;
}

.formulario {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

label {
  font-weight: bold;
  color: #3d1508;
  margin-top: 10px;
}

input[type="text"],
select {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
  font-size: 15px;
}

.opcionais {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.checkbox {
  font-weight: normal;
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: 0;
}

.btn-confirmar {
  margin-top: 20px;
  background: #7a2d10;
  color: #fff;
  border: none;
  padding: 14px;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}

.btn-confirmar:hover {
  background: #f0a500;
  color: #3d1508;
}
</style>