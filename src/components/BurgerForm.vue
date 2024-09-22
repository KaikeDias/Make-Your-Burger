<template>
    <div>
        <Message :msg="msg" v-show="msg"/>
        <div>
            <form id="burger-form" @submit="createBurguer">
                <div class="input-container">
                    <label for="name">Nome do cliente </label>
                    <input type="text" name="name" id="name" v-model="name" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="bread">Escolha o pão: </label>
                    <select name="bread" id="bread" v-model="bread">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="meat">Escolha a carne do seu Burguer:</label>
                    <select name="meat" id="meat" v-model="meat">
                        <option value="">Selecione o tipo de carne</option>
                        <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                    </select>
                </div>
                <div id="optionals-container" class="input-container">
                    <label id="optionals-title" for="optionals">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="optional in optionalsData" :key="optional.id">
                        <input type="checkbox" name="optionals" v-model="optionals" :value="optional.tipo">
                        <span>{{ optional.tipo }}</span>
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
import Message from './Message.vue';

    export default {
        name: "BurgerForm",
        components: {
            Message
        },
        data() {
            return {
                breads: null,
                meats: null,
                optionalsData: null,
                name: null,
                bread: "",
                meat: "",
                optionals: [],
                msg: null
            }
        },
        methods: {
            async getIngredients() {
                const req = await fetch("http://localhost:3000/ingredientes")
                const data = await req.json()

                this.breads = data.paes;
                this.meats = data.carnes;
                this.optionalsData = data.opcionais;


            },
            async createBurguer(e) {
                e.preventDefault()

                const data = {
                    name: this.name,
                    bread: this.bread,
                    meat: this.meat,
                    optionals: Array.from(this.optionals),
                    status: "Solicitado"
                }

                const dataJson = JSON.stringify(data)

                const req = await fetch("http://localhost:3000/burgers", {
                    method: "POST",
                    headers: {"Content-Type": "application/json"},
                    body: dataJson
                })

                const res = await req.json()

                this.msg = `Pedido realizado com sucesso`

                setTimeout(() => this.msg = "", 3000)

                this.name = ""
                this.meat = ""
                this.bread = ""
                this.optionals = []
            }
        },
        mounted() {
            this.getIngredients()
        }
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