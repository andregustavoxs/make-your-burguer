<template>
  <div id="burguer-table">
    <Message :msg="msg" v-show="msg"/>
    <div>
      <div id="burger-table-heading">
        <div class="order-id">#:</div>
        <div>Cliente:</div>
        <div>Pão:</div>
        <div>Carne:</div>
        <div>Opcionais:</div>
        <div>Ações:</div>
      </div>
    </div>
    <div id="burger-table-rows">
      <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
        <div class="order-number">{{ burger.id }}</div>
        <div>{{ burger.nome }}</div>
        <div>{{ burger.pao }}</div>
        <div>{{ burger.carne }}</div>
        <div>
          <ul>
            <li v-for="(opcional, index) in burger.opcionais" :key="index">{{ opcional }}</li>
          </ul>
        </div>
        <div>
          <select name="status" class="status" @change="updatedBurger($event, burger.id)">
            <option value="">Selecione</option>
            <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status === s.tipo">{{ s.tipo }}</option>
          </select>
          <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";

export default {
  name: "Dashboard",
  components: {Message},
  data() {
    return {
      burgers: null,
      burger_id: null,
      status: [],
      msg: null,
    }
  },
  methods: {
    async getPedidos() {
      const req = await fetch("http://localhost:3000/burgers");

      const data = await req.json();

      this.burgers = data;

      await this.getStatus();
    },
    async getStatus() {
      const req = await fetch("http://localhost:3000/status");

      const data = await req.json();

      this.status = data;
    },
    async deleteBurger(id) {
      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "DELETE"
      });

      const res = await req.json();

      // colocar uma msg de sistema
      this.msg = `O pedido N° ${id} foi removido com sucesso!`;

      // limpar msg
      setTimeout(() => this.msg = "", 3000);

      await this.getPedidos();
    },
    async updatedBurger(event, id) {

      const option = event.target.value;

      const dataJson = JSON.stringify({ status: option });

      const req = await fetch(`http://localhost:3000/burgers/${id}`, {
        method: "PATCH",
        headers: {"Content-Type": "application/json"},
        body: dataJson,
      });

      const res = await req.json();

      // colocar uma msg de sistema
      this.msg = `O pedido N° ${res.id} foi atualizado para ${res.status}!`;

      // limpar msg
      setTimeout(() => this.msg = "", 3000);
    }
  },
  mounted() {
    this.getPedidos();
  }
}
</script>

<style scoped>
#burger-table {
  max-width: 1200px;
  margin: 0 auto;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
}

#burger-table-heading {
  font-weight: bold;
  padding: 16px;
  border-bottom: 3px solid #FCBA03;
  background-color: #222;
  color: #fff;
  border-radius: 6px 6px 0 0;
}

#burger-table-heading div,
.burger-table-row div {
  width: 19%;
  padding: 0 10px;
}

.burger-table-row {
  width: 100%;
  padding: 16px;
  border-bottom: 1px solid #eee;
  transition: background-color 0.3s ease;
}

.burger-table-row:hover {
  background-color: #f9f9f9;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
  width: 5%;
  font-weight: bold;
}

.burger-table-row ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.burger-table-row ul li {
  background-color: #f0f0f0;
  margin: 2px 0;
  padding: 4px 8px;
  border-radius: 4px;
  font-size: 0.9em;
}

select.status {
  padding: 8px 12px;
  margin-right: 12px;
  border: 2px solid #ddd;
  border-radius: 4px;
  background-color: white;
  font-size: 14px;
  cursor: pointer;
  transition: all 0.3s ease;
}

select.status:hover {
  border-color: #FCBA03;
}

select.status:focus {
  outline: none;
  border-color: #FCBA03;
  box-shadow: 0 0 0 2px rgba(252, 186, 3, 0.2);
}

.delete-btn {
  background-color: #222;
  color: #FCBA03;
  font-weight: bold;
  border: 2px solid #222;
  padding: 8px 16px;
  font-size: 14px;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.delete-btn:hover {
  background-color: transparent;
  color: #222;
  transform: translateY(-1px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}
</style>