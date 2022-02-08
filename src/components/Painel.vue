<template>
  <div id="icecream-painel">
    <Message :mensagem="mensagem" v-show="mensagem"/>
    <div>
      <div id="icecream-painel-header">
        <div id="order-id">#</div>
        <div>Cliente:</div>
        <div>Recipiente:</div>
        <div>Sorvete:</div>
        <div>Adicional:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="icecream-painel-rows">
      <div
        class="icecream-painel-row"
        v-for="sorvete in sorvetes"
        :key="sorvete.id"
      >
        <div class="order-number">{{ sorvete.id }}</div>
        <div>{{ sorvete.nome }}</div>
        <div>{{ sorvete.recipiente }}</div>
        <div>{{ sorvete.sorvete }}</div>
        <div>{{ sorvete.adicional }}</div>
        <div>
          <select name="status" class="status" @change="updateSorvete($event, sorvete.id)">
            <option
              v-for="stts in status"
              :key="stts.id"
              :value="stts.tipo"
              :selected="sorvete.status == stts.tipo"
            >
              {{ stts.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deletePedido(sorvete.id)">
            Deletar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from './Message.vue'

export default {
  name: "Painel",
  components:{
    Message
    },
  data() {
    return {
      sorvetes: null,
      sorvetes_id: null,
      status: [],
      mensagem: null
    }
  },
  methods: {
    async getPedidos() {
      const req = await fetch('http://localhost:3000/FinalSorvetes')
        const data = await req.json()
        this.sorvetes = data
        this.getStatus()
    },

    async getStatus() {
      const req = await fetch("http://localhost:3000/status");
      const data = await req.json();

      this.status = data;
    },
    async deletePedido(id) {

        const req = await fetch(`http://localhost:3000/FinalSorvetes/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()

          this.mensagem = "Pedido removido!"
    setTimeout(() => this.mensagem = "", 6000)

        this.getPedidos()
    },
    async updateSorvete(event, id){
      const option = event.target.value
      const dataJSON = JSON.stringify({status:option})
      const req =await fetch(`http://localhost:3000/FinalSorvetes/${id}`,{
      method: "PATCH",
      headers:{"Content-Type": "application/json"},
      body: dataJSON })

      const res = await req.json()

                this.mensagem = `Pedido número ${res.id} foi alterado para ${res.status}!`
    setTimeout(() => this.mensagem = "", 6000)
    }
    },
    mounted() {
      this.getPedidos();
    },
}
</script>

<style scoped>
#icecream-painel {
  max-width: 1200px;
  margin: 0 auto;
}

#icecream-painel-header,
#icecream-painel-rows,
.icecream-painel-row {
  display: flex;
  flex-wrap: wrap;
}
#icecream-painel-header {
  font-weight: bold;
  padding: 15px;
  border-bottom: 5px solid;
}

#icecream-painel-header div,
.icecream-painel-row div {
  width: 16%;
}

.icecream-painel-row {
  width: 100%;
  padding: 12px;
  border-bottom: 2px solid;
}

select {
  padding: 10px 2px;
  margin-right: 10px;
  background-color: pink;
  border: 1px black solid;
  margin-bottom: 4px;
}

.delete-btn {
  cursor: pointer;
  background-color: pink;
  padding: 5px;
  margin: 0 auto;
  border: 1px black solid;
  margin-top: 4px;
}
</style>