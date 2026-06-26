<template>
  <div v-if="visivel" :class="['alerta', tipo]">
    <span class="icone">{{ icones[tipo] }}</span>
    <span class="mensagem">{{ mensagem }}</span>
  </div>
</template>

<script>
export default {
  name: "AlertaComponent",
  props: {
    visivel: {
      type: Boolean,
      default: false,
    },
    tipo: {
      type: String,
      default: "info",
    },
    mensagem: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      icones: {
        erro: "❌",
        aviso: "⚠️",
        info: "ℹ️",
        sucesso: "✅",
      },
    };
  },
};
</script>

<style scoped>
.alerta {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 14px 20px;
  border-radius: 8px;
  margin: 15px auto;
  max-width: 600px;
  font-weight: 500;
  border-left: 6px solid;
}

.icone {
  font-size: 20px;
}

/* Vermelho: erros de preenchimento */
.erro {
  background: #fdecea;
  border-color: #e53935;
  color: #b71c1c;
}

/* Laranja: alertas e avisos */
.aviso {
  background: #fff8e1;
  border-color: #f57c00;
  color: #e65100;
}

/* Azul: informações */
.info {
  background: #e3f2fd;
  border-color: #1976d2;
  color: #0d47a1;
}

/* Verde: sucesso */
.sucesso {
  background: #e8f5e9;
  border-color: #43a047;
  color: #1b5e20;
}
</style>