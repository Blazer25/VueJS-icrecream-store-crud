<template>
  <div>
    <h1 class="title">Monte seu Sorvete</h1>
        <Message :mensagem="mensagem" v-show="mensagem"/>
    <div>
      <form id="sorvete-form" method="POST" @submit="makeicecream">
        <div class="input-container">
          <label class="screen-only" for="nome">Nome do Cliente:</label>
          <p>Nome do Cliente:</p>
          <input
            type="text"
            id="nome"
            name="nome"
            v-model="nome"
            placeholder="Digite aqui o seu nome"
          />
        </div>
        <div class="input-container">
          <label class="screen-only" for="recipiente"
            >Escolha o Recipiente:</label
          >
          <p>Escolha o Recipiente:</p>

          <select name="recipiente" id="recipiente" v-model="recipiente">
            <option value="">Selecione o Recipiente</option>
            <option
              v-for="recipiente in recipientes"
              :key="recipiente.id"
              :value="recipiente.tipo"
            >
              {{ recipiente.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label class="screen-only" for="recipiente">Escolha o Sorvete:</label>
          <p>Escolha o Sorvete:</p>
          <select name="sorvetes" id="sorvetes" v-model="sorvete">
            <option value="">Selecione o Sorvete</option>
            <option
              v-for="sorvete in sorvetesData"
              :key="sorvete.id"
              :value="sorvete.tipo"
            >
              {{ sorvete.tipo }}
            </option>
            <!-- <option value="1">Chocolate</option> -->
          </select>
        </div>

        <div class="input-container">
          <label class="screen-only" for="recipiente"
            >Escolha o Adicional:</label
          >
          <p>Escolha o Adicional:</p>
          <select name="adicional" id="adicional" v-model="adicional">
            <option value="">Selecione o Adicional</option>
            <option
              v-for="adicional in adicionaisData"
              :key="adicional.id"
              :value="adicional.tipo"
            >
              {{ adicional.tipo }}
            </option>
          </select>
        </div>

        <div class="input-container">
          <input
            id="btnsend"
            type="submit"
            class="submit-btn"
            value="Montar Sorvete"
          />
        </div>
      </form>
    </div>
  </div>
</template>

<script>
  import Message from './Message.vue'

export default {
  name: "FormSorvete",
  components:{
    Message
  },
  data() {
    return {
      //Dados que são buscados no Server/DB
      recipientes: null,
      sorvetesData: null,
      adicionaisData: null,

      //Dados que são passados do form para o servidor
      nome: null,

      recipiente: null,
      sorvete: null,
      adicional: null,

      status: "Solicitado",
      mensagem: null,
    };
  },
  methods: {
    async getIngredients() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json();

      this.recipientes = data.recipiente;
      this.sorvetesData = data.sorvete;
      this.adicionaisData = data.adicional;
    },
    async makeicecream(e) {
      e.preventDefault();

      const dataForm = {
        nome: this.nome,

        recipiente: this.recipiente,
        sorvete: this.sorvete,
        adicional: this.adicional,

        status: "Solicitado",
      };
      const dataJson = JSON.stringify(dataForm);
      const req = await fetch("http://localhost:3000/FinalSorvetes", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: dataJson,
      });

    this.mensagem = "Pedido Realizado :D"
    setTimeout(() => this.mensagem = "", 6000)

      console.log(req);
      const res = await req.json();
      console.log(res);
    },
  },
  mounted() {
    this.getIngredients();
  },
};
</script>

<style scoped>
.title {
  margin-bottom: 25px;
  margin-top: 30px;
}

#sorvete-form {
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 25px;
}

p {
  font-weight: bold;
  margin-bottom: 8px;
  padding: 5px 5px;
  border-left: 4px solid pink;
  margin-left: 51px;
}

input,
select {
  margin: 0 auto;
  padding: 5px 5px;
  width: 300px;
  border: 2px solid black;
  border-radius: 2px;
}

.submit-btn {
  cursor: pointer;
  background-color: pink;
  font-weight: bold;
  font-size: medium;
  padding: 10px;
  margin: 0 auto;
  transition: 0.7s;
}

.submit-btn:hover {
  background-color: #dd429c;
}
</style>