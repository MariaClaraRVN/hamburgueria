<template>
  <Mensage :msg="msg" v-show="msg" />
  <div id="burguer-table">
    <div>
      <div id="burguer-table-heading">

        <div class="order-id">Id:</div>

        <div>Cliente:</div>

        <div>Pão:</div>

        <div>Carne:</div>

        <div>Opcionais:</div>

        <div>Molhos:</div>

        <div>Queijos:</div>

        <div>Ações</div>

      </div>
    </div>
    <div id="burguer-table-rows">

      <div class="burguer-table-row" v-for="burguer in burguers" :key="burguer.id">

        <div class="order-number">{{ burguer.id }}</div>
        <div>{{ burguer.nome }}</div>

        <div>{{ burguer.pao }}</div>

        <div>{{ burguer.carne }}</div>

        <div>
          <ul>
            <li v-for="(opcional, index) in burguer.opcionais" :key="index">{{ opcional }}</li>
          </ul>
        </div>

        <div>
          <ul>
            <li v-for="(molho, index) in burguer.molhos" :key="index">{{ molho }}</li>
          </ul>
        </div>

        <div>
          <ul>
            <li v-for="(queijo, index) in burguer.queijos" :key="index">{{ queijo }}</li>
          </ul>
        </div>

        <div>
          <select name="status" class="status" @change="updateBurguer($event, burguer.id)">
            <option value="">Selecione</option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burguer.status == s.tipo">
              {{ s.tipo }}
            </option>
          </select>
          <button class="delete-btn" @click="deleteBurguer(burguer.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Mensage from './Mensage.vue';

export default {
  name: 'Dashboard',
  components:{
    Mensage
  },
  data() {
    return {
      burguers: null,
      burguer_id: null,
      status: [],
      msg: null,
    }
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");

      const data = await req.json();

      this.burguers = data;

      this.getStatus();

    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status = data;
    },

    async deleteBurguer(id) {

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE"
      });

      const res = await req.json();

      this.msg = `Pedido de ${res.nome} removido com sucesso!`;
      setTimeout(() => this.msg = "", 3500);


      this.getPedidos();
    },
    async updateBurguer(vent, id) {
      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option});

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      });

      const res = await req.json();

      this.msg = `Pedido de ${res.nome} atualizado para ${res.status}!`;
      setTimeout(() => this.msg = "", 3500);
    }

  },
  mounted() {
    this.getPedidos();
  }
}
</script>



<style scoped>
#burguer-table {
  max-width: 1200px;
  margin: 0 auto;
  font-family: 'Arial', sans-serif;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

#burguer-table-heading,
#burguer-table-rows,
.burguer-table-row {
  display: flex;
  flex-wrap: nowrap;
}

#burguer-table-rows {
  display: flex;
  flex-direction: column;
}

#burguer-table-heading {
  font-weight: bold;
  padding: 15px;
  border-bottom: 3px solid #333;
  background-color: #fcba03;
  color: #222;
  border-radius: 8px 8px 0 0;
}

#burguer-table-heading div,
.burguer-table-row div {
  width: 19%;
  padding: 10px;
}

.burguer-table-row {
  width: 100%;
  padding: 15px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s ease;
}

.burguer-table-row:hover {
  background-color: #f1f1f1;
}

#burguer-table-heading .order-id,
.burguer-table-row .order-number {
  width: 7%;
}

select.status {
  padding: 8px 12px;
  margin-right: 12px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 14px;
  background-color: #fff;
  cursor: pointer;
  margin-bottom: 2%;
}

.delete-btn {
  background-color: #ff4444;
  color: #fff;
  font-weight: bold;
  border: none;
  padding: 10px 20px;
  font-size: 14px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.delete-btn:hover {
  background-color: #cc0000;
}

ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

ul li {
  padding: 5px 0;
  font-size: 14px;
  color: #555;
}

@media (max-width: 820px) {

#burguer-table-heading,
.burguer-table-row {
  flex-wrap: wrap;
}

#burguer-table-heading div,
.burguer-table-row div {
  width: 100%;
  text-align: center;
  padding: 5px;
}

.delete-btn {
  width: 100%;
  margin-top: 10px;
}
}
</style>