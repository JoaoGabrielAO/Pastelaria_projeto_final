<template>
  <div class="pedidos">
    <h1>Pedidos Realizados</h1>

    <AlertaComponent
      :visivel="alerta.visivel"
      :tipo="alerta.tipo"
      :mensagem="alerta.mensagem"
    />

    <p v-if="pedidos.length === 0" class="vazio">
      Nenhum pedido por enquanto. Que tal fazer o primeiro? 🥟
    </p>

    <div class="lista">
      <div class="pedido-card" v-for="pedido in pedidos" :key="pedido.id">
        <div class="info">
          <h3>{{ pedido.sabor }}</h3>
          <p><strong>Cliente:</strong> {{ pedido.cliente }}</p>
          <p><strong>Tamanho:</strong> {{ pedido.tamanho }}</p>
          <p v-if="pedido.opcionais && pedido.opcionais.length">
            <strong>Opcionais:</strong> {{ pedido.opcionais.join(", ") }}
          </p>
        </div>
        <button class="btn-excluir" @click="excluirPedido(pedido.id)">
          Excluir
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import AlertaComponent from "@/components/AlertaComponent.vue";
import { API_URL } from "@/api.js";

export default {
  name: "PedidosView",
  components: {
    AlertaComponent,
  },
  data() {
    return {
      pedidos: [],
      alerta: {
        visivel: false,
        tipo: "info",
        mensagem: "",
      },
    };
  },
  mounted() {
    this.carregarPedidos();
  },
  methods: {
    carregarPedidos() {
      fetch(`${API_URL}/pedidos`)
        .then((r) => r.json())
        .then((dados) => {
          this.pedidos = dados;
        });
    },
    excluirPedido(id) {
      fetch(`${API_URL}/pedidos/` + id, {
        method: "DELETE",
      }).then(() => {
        this.pedidos = this.pedidos.filter((p) => p.id !== id);
        this.mostrarAlerta("sucesso", "Pedido excluído com sucesso!");
      });
    },
    mostrarAlerta(tipo, mensagem) {
      this.alerta.tipo = tipo;
      this.alerta.mensagem = mensagem;
      this.alerta.visivel = true;
    },
  },
};
</script>

<style scoped>
.pedidos {
  padding: 30px;
  max-width: 700px;
  margin: 0 auto;
}

.pedidos h1 {
  color: #7a2d10;
  text-align: center;
}

.vazio {
  text-align: center;
  color: #777;
  margin-top: 30px;
  font-size: 18px;
}

.lista {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: 20px;
}

.pedido-card {
  background: #fff;
  border: 2px solid #f0a500;
  border-radius: 12px;
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.info h3 {
  color: #7a2d10;
  margin-bottom: 8px;
}

.info p {
  color: #555;
  margin: 3px 0;
  font-size: 14px;
}

.btn-excluir {
  background: #e53935;
  color: #fff;
  border: none;
  padding: 10px 18px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 15px;
}

.btn-excluir:hover {
  background: #b71c1c;
}
</style>