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
                <button type="submit">Enviar informações</button>
        </form>
    </div>
</template>
