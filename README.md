🥟 Pastelaria do João

Sistema de pedidos online para uma pastelaria, desenvolvido em Vue 3.
O projeto foi adaptado a partir da base do sistema T-Burguer, mudando o
modelo de negócio de hamburgueria para pastelaria.

🔗 Links


Site publicado: https://joaogabrielao.github.io/Pastelaria_projeto_final/
API (JSON Server / Render): https://pastelaria-banco-json.onrender.com
Repositório do código: https://github.com/JoaoGabrielAO/Pastelaria_projeto_final
Repositório do banco (JSON): https://github.com/JoaoGabrielAO/pastelaria-banco-json


📋 Visão Geral

O segmento escolhido foi uma pastelaria. Em vez de hambúrgueres, o
cliente escolhe o sabor do pastel, o tamanho (Individual, Grande
ou Família) e opcionais (borda de catupiry, queijo extra, bacon e
molho da casa).

Principais alterações feitas em relação ao projeto original:


Nova identidade visual (nome, cores marrom/laranja e emoji 🥟) na NavBar
e no Banner.
Cardápio de pastéis carregado dinamicamente da API.
Formulário de pedido adaptado ao tema (sabor, tamanho e opcionais).
Validação de campos obrigatórios antes de confirmar o pedido.
Componente de alertas semânticos reutilizável.
Listagem de pedidos com exclusão em tempo real.


🚨 Lógica dos Alertas Semânticos

Foi criado um componente reutilizável (AlertaComponent.vue) que recebe
três informações via props: se está visível, o tipo do alerta e a
mensagem. Dependendo do tipo, ele aplica uma classe de cor diferente:

CorTipoQuando aparece🔴 VermelhoerroCampo obrigatório vazio ou ação inválida🟠 LaranjaavisoAvisos importantes🔵 AzulinfoInformações gerais🟢 VerdesucessoPedido cadastrado ou excluído com sucesso

Exemplo de como o alerta é usado na tela:

vue<AlertaComponent
  :visivel="alerta.visivel"
  :tipo="alerta.tipo"
  :mensagem="alerta.mensagem"
/>

A validação acontece no método confirmarPedido(). Se um campo
obrigatório estiver vazio, o alerta é exibido e o envio é bloqueado com
return:

javascriptif (!this.pedido.cliente) {
  this.mostrarAlerta("erro", "Por favor, informe o nome do cliente.");
  return;
}

Quando o pedido é salvo com sucesso, é exibido o alerta verde e o usuário
é redirecionado automaticamente para a tela de pedidos:

javascriptthis.mostrarAlerta("sucesso", "Pedido confirmado com sucesso!");
setTimeout(() => {
  this.$router.push({ name: "pedidos" });
}, 1500);

🛠️ Tecnologias


Vue 3
Vue Router
JSON Server (API mockada)
GitHub Pages (deploy do front-end)
Render (deploy da API)


▶️ Como rodar localmente

bash# instalar dependências
npm install

# rodar o front-end
npm run serve

# em outro terminal, rodar a API local
npx json-server --watch db/db.json --port 3000


Para rodar localmente, ajuste a URL em src/api.js para
http://localhost:3000.