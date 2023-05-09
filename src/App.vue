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
  },
})
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
              <button v-if="isEditing" type="submit">Editar</button>
              <button v-if="isEditing" type="button" @click="cancelEdit">Cancelar</button>
      </form> 
    </div>
    <div class="user-cards">
    <div v-for="(user, key) in users" :key="key" class="card">
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
      </div>
    </div>
  </div>
</template>
<style>
  .formulario {
    color:#000000;
    padding: 20px;
    background: linear-gradient(to right, rgb(255, 228, 230), rgb(204, 251, 241));
    border-radius: 20px;
  }

  form {
    max-width: 500px;
    margin: 0 auto;
  }

  label {
    font-weight: bold;
    margin-bottom: 5px;
    display: block;
  }
  input[type="text"],
  input[type="email"],
  input[type="password"],
  select,
  textarea {
    width: 100%;
    padding: 8px;
    margin-bottom: 10px;
    border: none;
    border-radius: 4px;
    box-sizing: border-box;
    border: solid 1px #e97bf7;
    background: conic-gradient(at left center, rgb(254, 246, 224), rgb(231, 205, 255), rgb(198, 215, 242));
    color: #000000;
  }

  button {
    padding: 10px 20px;
    background-color: #4caf50;
    color: #fff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  .user-cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  .card {
    width: calc(50% - 10px);
    margin-bottom: 20px;
    padding: 10px;
    background-color: #fff;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
  }

  .card-content {
    margin-bottom: 10px;
  }

  .card-content div {
    margin-bottom: 5px;
  }

  .card-content strong {
    font-weight: bold;
  }
</style>