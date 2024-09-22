<template>
    <div>
        <p>Componente de Mensagem</p>
        <div>
            <form id="burger-form">
                <div class="input-container">
                    <label for="name">Nome do cliente </label>
                    <input type="text" name="name" id="name" v-model="name" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="bread">Escolha o pão: </label>
                    <select name="bread" id="bread" v-model="bread">
                        <option value="">Selecione o seu pão</option>
                        <option value="integral">Integral</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="meat">Escolha a carne do seu Burguer:</label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="">Selecione o tipo de carne</option>
                        <option value="integral">Integral</option>
                    </select>
                </div>
                <div id="optionals-container" class="input-container">
                    <label id="optionals-title" for="optionals">Selecione os opcionais:</label>
                    <div class="checkbox-container">
                        <input type="checkbox" name="optionals" v-model="optionals" value="salame">
                        <span>Salame</span>
                    </div>
                    <div class="checkbox-container">
                        <input type="checkbox" name="optionals" v-model="optionals" value="salame">
                        <span>Salame</span>
                    </div>
                    <div class="checkbox-container">
                        <input type="checkbox" name="optionals" v-model="optionals" value="salame">
                        <span>Salame</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="btn-submit" value="Criar meu Burguer">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
    export default {
    
    } 
</script>

<style scoped>
    #burger-form {
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
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    input, select {
        padding: 5px 10px;
        width: 300px;
    }

    #optionals-container {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
    }

    #optionals-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: center;
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

    .btn-submit {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .btn-submit:hover {
        background-color: transparent;
        color: #222;
    }
</style>