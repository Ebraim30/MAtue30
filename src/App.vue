<template>
    <div class="formulario">
        <form action="submitForm">
            <div class="input-name">
                <label for="name">Nome</label>
                <input type="text" placeholder="Digite o nome"></div>
                <div class="input-email">
                <label for="email">Email:</label>
                <input type="email" placeholder="Digite seu email"></div>
                <div class="input-pass">
                <label for="password">Senha:</label>
                <input type="password" placeholder="Digite sua senha"></div>
                <div class="input-pass">
                <label for="password">Senha2:</label> 
                <input type="password" placeholder="Confirme sua senha"></div>
                <div class="input-date">
                <label for="date">Data:</label> 
                <input type="date" placeholder="Date"></div>
                <div class="input-endereço">
                <label for="text">endereço</label>   
                <input type="text" placeholder="Digite seu endereço"></div>
                <div class="input-string">
                <label for="string">Cidade</label>  
                <input type="string" placeholder="Digite sua cidade"></div>
                <label for="string">Estado</label> 
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
                <label for="string">Hobbie</label>  
                <input type="string" placeholder="Digite seu Hobbie"></div>
                <label for="string">Linguagem</label> 
                <select v-model="lingua">
                <option value="JavaScript">JavaScript</option>
                <option value="C++">C++</option>
                <option value="Python">Python</option>
                <option value="Java">Java</option>
                <option value="C#">C#</option>
                </select>
                <p>Biografia:</p>
                <textarea v-model="biografia" cols="50" rows="10"></textarea>
                <br>
                <button type="submit">Enviar informações</button>
        </form>
    </div>
</template>
