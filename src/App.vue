<script>
import { defineComponent } from 'vue'


export default defineComponent({
  data() {
    return {
      name: "",
      email: "",
      password: "",
      confpass:"",
      data: "",
      endereco: "",
      cidade: "",
      estado: "",
      hobbie: "",
      linguagem: "",
      biografia: "",
      users: {},
      isEditing: false,
      editingUserKey: null,
    }
  },
  created() {
    this.getUsers()
  },
  methods: {
    getUsers() {
      const users = { ...localStorage }
      for (const key in users) {
        try {
          const userObj = JSON.parse(users[key])
          this.users[key] = userObj
        } catch (e) {
        }
      }
    },
    submitForm() {
      if (this.isEditing && this.editingUserKey) {
        const user = {
          name: this.name,
          email: this.email,
          password: this.password,
          confpass: this.confpass,
          data: this.data,
          endereco: this.endereco,
          cidade: this.cidade,
          estado: this.estado,
          hobbie: this.hobbie,
          linguagem: this.linguagem,
          biografia: this.biografia,
        }
        localStorage.setItem(this.editingUserKey, JSON.stringify(user))
        this.isEditing = false
        this.editingUserKey = null
      } else {
        const user = {
          name: this.name,
          email: this.email,
          password: this.password,
          confpass: this.confpass,
          data: this.data,
          endereco: this.endereco,
          cidade: this.cidade,
          estado: this.estado,
          hobbie: this.hobbie,
          linguagem: this.linguagem,
          biografia: this.biografia,
        }
        localStorage.setItem(user.email, JSON.stringify(user))
      }
      this.getUsers()
      this.name = ""
      this.email = ""
      this.password = ""
      this.confpass = ""
      this.data = ""
      this.endereco = ""
      this.cidade = ""
      this.estado = ""
      this.hobbie = ""
      this.linguagem = ""
      this.biografia = ""
    },
    deleteUser(key) {
      localStorage.removeItem(key)
      delete this.users[key]
    },
    editUser(user) {
      this.name = user.name
      this.email = user.email
      this.password = user.password
      this.confpass = user.confpass
      this.data = user.data
      this.endereco = user.endereco
      this.cidade = user.cidade
      this.estado = user.estado
      this.hobbie = user.hobbie
      this.biografia = user.biografia
      this.linguagem = user.linguagem
      this.isEditing = true
      this.editingUserKey = user.email
    },
    cancelEdit() {
      this.isEditing = false
      this.editingUserKey = null
      this.name = ""
      this.email = ""
      this.password = ""
      this.confpass = ""
      this.data = ""
      this.endereco = ""
      this.cidade = ""
      this.estado = ""
      this.hobbie = ""
      this.linguagem = ""
      this.biografia = ""
    },
    }
  },
)

anonimo (hide)
</script>
<template>
  <div class="formulario">
      <form @submit.prevent="submitForm">
          <div class="input-name">
              <label for="name">Nome</label>
              <input type="text" placeholder="Digite o nome" v-model="name"></div>
              <div class="input-email">
              <label for="email">Email:</label>
              <input type="email" placeholder="Digite seu email" v-model="email"></div>
              <div class="input-pass">
              <label for="password">Senha:</label>
              <input type="password" placeholder="Digite sua senha" v-model="password"></div>
              <div class="input-pass">
              <label for="password">Confirme sua senha: </label> 
              <input type="password" placeholder="Confirme sua senha" v-model="confpass"></div>
              <div class="input-date">
              <label for="date">Data:</label> 
              <input type="date" placeholder="Date" v-model="data"></div>
              <div class="input-endereço">
              <label for="text">endereço</label>   
              <input type="text" placeholder="Digite seu endereço" v-model="endereco"></div>
              <div class="input-string">
              <label for="cidade">Cidade</label>  
              <input type="text" placeholder="Digite sua cidade" v-model="cidade"></div>
              <label for="text">Estado</label> 
              <select v-model="estado">
              <option value="AC">Acre</option>
              <option value="AL">Alagoas</option>
              <option value="AP">Amapá</option>
              <option value="AM">Amazonas</option>
              <option value="BA">Bahia</option>
              <option value="CE">Ceará</option>
              <option value="DF">Distrito Federal</option>
              <option value="ES">Espírito Santo</option>
              <option value="GO">Goiás</option>
              <option value="MA">Maranhão</option>
              <option value="MT">Mato Grosso</option>
              <option value="MS">Mato Grosso do Sul</option>
              <option value="MG">Minas Gerais</option>
              <option value="PA">Pará</option>
              <option value="PB">Paraíba</option>
              <option value="PR">Paraná</option>
              <option value="PE">Pernambuco</option>
              <option value="PI">Piauí</option>
              <option value="RJ">Rio de Janeiro</option>
              <option value="RN">Rio Grande do Norte</option>
              <option value="RS">Rio Grande do Sul</option>
              <option value="RO">Rondônia</option>
              <option value="RR">Roraima</option>
              <option value="SC">Santa Catarina</option>
              <option value="SP">São Paulo</option>
              <option value="SE">Sergipe</option>
              <option value="TO">Tocantins</option></select>
              <div class="input-string">
              <label for="text">Hobbie</label>  
              <input type="text" placeholder="Digite seu Hobbie" v-model="hobbie"></div>
              <label for="text">Linguagem</label> 
              <select v-model="linguagem">
              <option value="JavaScript">JavaScript</option>
              <option value="C++">C++</option>
              <option value="Python">Python</option>
              <option value="Java">Java</option>
              <option value="C#">C#</option>
              </select>
              <p>Biografia:</p>
              <textarea v-model="biografia" cols="50" rows="10"></textarea>
              <br>
              <button v-if="!isEditing" type="submit">Registrar</button>
              <button v-if="isEditing" type="submit">Confirmar</button>
              <button v-if="isEditing" type="button" @click="cancelEdit">Cancelar</button>
      </form> 
    </div>
    <div class="user-cards">

    <div v-for="(user, key, hide) in users" :key="key" class="card">
      <div class="card-content">
        <div><strong>Nome:</strong> {{ user.name }}</div>
        <div><strong>E-mail:</strong> {{ user.email }}</div>
        <div><strong>Senha:</strong> {{ user.password }}</div>
        <div><strong>Estado:</strong> {{ user.estado }}</div>
        <div><strong>Endereço:</strong> {{ user.endereco }}</div>
        <div><strong>Estado:</strong> {{ user.estado }}</div>
        <div><strong>Cidade:</strong> {{ user.cidade }}</div>
        <div><strong>Hobbie:</strong> {{ user.hobbie }}</div>
        <div><strong>Linguagem:</strong> {{ user.linguagem }}</div>
        <div><strong>Biografia:</strong> {{ user.biografia }}</div>

      </div>
      <div>
        <button @click="editUser(user)">Editar</button>
        <button @click="deleteUser(key)">Excluir</button>
        <button @click="anonimo(hide)">Anonimo</button>
      </div>
    </div>
  </div>
</template>
<style>

  .formulario {
    max-width: 1000px;
    margin: 0 auto;
    padding: 40px;
    background-color: #0099ff;
    border-radius: 5px;
    color: #000000;
  }

  .formulario label {
    display: block;
    font-weight: bold;
    margin-bottom: 10px;
  }

  .formulario input[type="text"],
  .formulario input[type="email"],
  .formulario input[type="password"],
  .formulario input[type="date"],
  .formulario select,
  .formulario textarea {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border-radius: 3px;
    border: 1px solid #000000;
  }

  .formulario button {
    padding: 10px 20px;
    margin-top: 10px;
    border-radius: 3px;
    border: none;
    color: #000000;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

 
  .formulario button[type="submit"] {
    background-color: #00ffea; 
  }

  .formulario button[type="submit"]:hover {
    background-color: #45a049; 
  }

  .formulario button[type="button"] {
    background-color: #ff9800;
  }

  .formulario button[type="button"]:hover {
    background-color: #e68a00; 
  }

  
  .user-cards {
    display: flow-root;
    flex-wrap: wrap;
    justify-content: flex-end;
    margin-top: 20px;
  }

  .card {
    flex: 0 0 300px;
    background-color: #8900fa;
    border-radius: 15px;
    box-shadow: 0 2px 4px rgb(255, 0, 0);
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .card-content {
    padding: 30px;
  }

  .card button {
    padding: 5px 10px;
    margin-top: 10px;
    border-radius: 3px;
    border: none;
    color: #4b398b;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .card button.edit {
    background-color: #ffeb3b; 
  }

  .card button.edit:hover {
    background-color: #fdd835; 
  }

  .card button.delete {
    background-color: #f44336; 
  }

  .card button.delete:hover {
    background-color: #e53935; 
  }
</style>
