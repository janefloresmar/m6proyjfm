<template>
  <Message :msg="msg" v-show="msg" />
  <div>
    <form id="user-form" method="POST" @submit="createUser">
      <div class="input-container">
        <label for="id">ID Cliente:</label>
        <input type="text" id="id" name="id" v-model="id" placeholder="Ingrese ID">
      </div>
      <div class="input-container">
        <label for="nombre">Nombre:</label>
        <input type="text" id="nombre" name="nombre" v-model="nombre" placeholder="Ingrese Nombre">
      </div>
      <div class="input-container">
        <label for="direccion">Direccion:</label>
        <input type="text" id="direccion" name="direccion" v-model="direccion" placeholder="Ingrese Direccion">
      </div>
      <div class="input-container">
        <label for="celular">Celular:</label>
        <input type="text" id="celular" name="celular" v-model="celular" placeholder="Ingrese Celular">
      </div>
      
      <div class="input-container">
        <input class="submit-btn" type="submit" value="Enviar">
      </div>
    </form>
  </div>
</template>
<script>

import Message from './Message'
export default {
  name: "UserForm",
  data() {
    return {
      id: null,
      nombre: null,
      direccion: null,
      celular: null,
    }
  },
  methods: {
    async getIngredientes() {
      const req = await fetch('http://localhost:3000/ingredientes')
      const data = await req.json()
      this.paes = data.paes
      this.carnes = data.carnes
      this.opcionaisdata = data.opcionais
    },
    async createUser(e) {
      e.preventDefault()

      const data = {
       
        id:this.id,
        nombre: this.nombre,
        direccion: this.direccion,
        celular: this.celular,
      }
      const dataJson = JSON.stringify(data)    
    
        const req = await fetch("http://localhost:3000/persona", {
        method: "POST",
        headers: { "Content-Type" : "application/json" },
        body: dataJson
      });
      const res = await req.json()
      console.log(res)
      this.msg = "Se Agrego usuario correctamente!"
      setTimeout(() => this.msg = "", 3000)
      this.id="",
      this.nombre="",
      this.direccion="",
      this.celular=""
    }

  },
  mounted () {
    this.getIngredientes()
  },
  components: {
    Message
  }
}
</script>




<style scoped>
  #user-form {
    max-width: 400px;
    margin: 0 auto;
  }

  .input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }

  label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
  }

  input, select {
    padding: 5px 10px;
    width: 300px;
  }

  #opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
  }

  #opcionais-title {
    width: 100%;
  }

  .checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
  }

  .checkbox-container span,
  .checkbox-container input {
    width: auto;
  }

  .checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
  }

  .submit-btn {
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
  }

  .submit-btn:hover {
    background-color: transparent;
    color: #222;
  }
</style>