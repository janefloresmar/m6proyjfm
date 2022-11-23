<template>
 
    <div id="user-table" v-if="persona">
    <div>
      <div id="user-table-heading">
        <div class="order-id">#:</div>
        
        <div>Nombre:</div>
        <div>Direccion:</div>
        <div>Celular:</div>
        <div>Acciones:</div>
      </div>
    


      <div class="user-table-row" v-for="per in persona" :key="per.id">
        <div class="order-number">{{ per.id }}</div>
        <div>{{ per.nombre }}</div>
        <div>{{ per.direccion }}</div>
        <div>{{ per.celular }}</div>
        
        <div>
          
          <button class="delete-btn" @click="deleteUser(per.id)">Borrar</button>
        </div>
      </div>


    </div>
  </div>
  <div v-else>
    <h2>No existen usuarios registrados</h2>
  </div>
</template>


<script>
  export default {
    name: "Dashboard",
    data() {
      return {
        persona:null
      }
    },
    methods: {
      async getPedidos() {
        const req = await fetch('http://localhost:3000/persona')
        const data = await req.json()
        this.persona = data
        console.log('data',data)
      
      },
      
      async deleteUser(id) {
        const req = await fetch(`http://localhost:3000/persona/${id}`, {
          method: "DELETE"
        });
        const res = await req.json()
        this.getPedidos()
      }
      
    },
    mounted () {
    this.getPedidos()
    }
  }
</script>

<style scoped>
  #user-table {
    max-width: 1200px;
    margin: 0 auto;
  }

  #user-table-heading,
  #user-table-rows,
  .user-table-row {
    display: flex;
    flex-wrap: wrap;
  }

  #user-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
  }

  .user-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
  }

  #user-table-heading div,
  .user-table-row div {
    width: 19%;
  }

  #user-table-heading .order-id,
  .user-table-row .order-number {
    width: 5%;
  }

  select {
    padding: 12px 6px;
    margin-right: 12px;
  }

  .delete-btn {
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
  
  .delete-btn:hover {
    background-color: transparent;
    color: #222;
  }
  
</style>