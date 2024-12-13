<template>
  <div>
    <Message :msg="msg" v-show="msg"/>
    <div>
      <form id="burger-form" @submit="createBurger">
        <div class="input-container">
          <label for="nome">Nome do Cliente</label>
          <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite o seu nome">
        </div>
        <div class="input-container">
          <label for="pao">Escolha do pão:</label>
          <select name="pao" id="pao" v-model="pao">
            <option value="">Selecione o seu pão</option>
            <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
              {{ pao.tipo }}
            </option>
          </select>
        </div>
        <div class="input-container">
          <label for="carne">Escolha a carne do seu Burger:</label>
          <select name="carne" id="carne" v-model="carne">
            <option value="">Selecione o tipo de carne</option>
            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
              {{ carne.tipo }}
            </option>
          </select>
        </div>
        <div id="opcionais-container" class="input-container">
          <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
          <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
            <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
            <span>{{ opcional.tipo }}</span>
          </div>
        </div>
        <div class="input-container">
          <input type="submit" class="submit-btn" value="Criar meu Burger!">
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import Message from "@/components/Message.vue";

export default {
  name: "BurgerForm",
  components: {Message},
  data() {
    return {
      paes: null,
      carnes: null,
      opcionaisdata: null,
      nome: null,
      pao: null,
      carne: null,
      opcionais: [],
      msg: null,
    }
  },
  methods: {
    async getIngredientes() {
      const req = await fetch("http://localhost:3000/ingredientes");
      const data = await req.json(); // Converte em um objeto javascript

      this.paes = data.paes;
      this.carnes = data.carnes;
      this.opcionaisdata = data.opcionais;
    },
    async createBurger(e) {
      e.preventDefault();

      // Check if required fields are empty
      if (!this.nome || !this.pao || !this.carne) {
        this.msg = "Por favor, preencha todos os campos obrigatórios!";
        setTimeout(() => this.msg = "", 3000);
        return;
      }

      const data = {
        nome: this.nome,
        carne: this.carne,
        pao: this.pao,
        opcionais: Array.from(this.opcionais),
        status: "Solicitado",
      }

      const dataJson = JSON.stringify(data);

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json();

      // Colocar uma mensagem de sistema
      this.msg = "Pedido realizado com sucesso!";

      // Limpar mensagem após 3 segundos
      setTimeout(() => this.msg = "", 3000);

      // limpar os campos
      this.nome = "";
      this.carne = "";
      this.pao = "";
      this.opcionais = [];
    }
  },
  mounted() {
    this.getIngredientes();
  },
}
</script>

<style scoped>
#burger-form {
  max-width: 600px;
  margin: 2rem auto;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 1.5rem;
  position: relative;
}

label {
  font-weight: 600;
  margin-bottom: 0.8rem;
  color: #222;
  padding: 0.5rem 1rem;
  border-left: 4px solid #FCBA03;
  background-color: rgba(252, 186, 3, 0.1);
  border-radius: 0 4px 4px 0;
}

input, select {
  padding: 0.8rem 1rem;
  width: 100%;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
  transition: all 0.3s ease;
  background-color: #fff;
}

input:focus, select:focus {
  outline: none;
  border-color: #FCBA03;
  box-shadow: 0 0 0 3px rgba(252, 186, 3, 0.2);
}

input::placeholder {
  color: #999;
}

select {
  cursor: pointer;
  appearance: none;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24' fill='none' stroke='%23222' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 1rem center;
  background-size: 1em;
}

#opcionais-container {
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1rem;
  background-color: #f9f9f9;
  padding: 1.5rem;
  border-radius: 8px;
}

#opcionais-title {
  width: 100%;
  margin-bottom: 1rem;
}

.checkbox-container {
  display: flex;
  align-items: center;
  width: calc(50% - 0.5rem);
  margin-bottom: 0.8rem;
  padding: 0.5rem;
  background-color: white;
  border-radius: 6px;
  transition: transform 0.2s ease;
}

.checkbox-container:hover {
  transform: translateY(-2px);
}

.checkbox-container input[type="checkbox"] {
  width: 1.2rem;
  height: 1.2rem;
  margin-right: 0.5rem;
  cursor: pointer;
}

.checkbox-container span {
  margin-left: 0.5rem;
  font-weight: 500;
  color: #444;
}

.submit-btn {
  background-color: #222;
  color: #FCBA03;
  font-weight: 600;
  border: 2px solid #222;
  padding: 1rem 2rem;
  font-size: 1.1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  width: 100%;
  border-radius: 8px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-top: 1rem;
}

.submit-btn:hover {
  background-color: #FCBA03;
  border-color: #FCBA03;
  color: #222;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(252, 186, 3, 0.2);
}

@media (max-width: 600px) {
  #burger-form {
    margin: 1rem;
    padding: 1rem;
  }

  .checkbox-container {
    width: 100%;
  }

  input, select {
    width: 100%;
  }
}
</style>