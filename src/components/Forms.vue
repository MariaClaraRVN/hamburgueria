<template>
    <div>
        <Mensage :msg="msg" v-show="msg" />
        <div>
            <form action="" id="burguer-form" @submit="createBurguer">
                <h2 style="text-align: center; color: #222; margin-bottom: 20px;">Monte seu Hambúrguer</h2>
                <!-- Nome do cliente -->
                <div class="input-form">
                    <label for="nome">
                        Nome do cliente
                    </label>
                    <input type="text" name="nome" id="nome" v-model="nome" placeholder="Digite seu nome">
                </div>

                <!-- Escolha do pão -->
                <div class="input-form">
                    <label for="pao">
                        Escolha seu pão:
                    </label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                    </select>
                </div>

                <!-- Escolha da carne -->
                <div class="input-form">
                    <label for="carne">
                        Escolha sua carne:
                    </label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione a sua carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{ carne.tipo }}</option>
                    </select>
                </div>

                <!-- Escolha seus opcionais -->
                <div class="input-form" id="opcionais">
                    <label for="opcionais" id="opcionais-title">
                        Selecione os opcionais:
                    </label>
                    <div class="checkbox" v-for="opicional in opcionaisdata" :key="opicional.id">
                        <input type="checkbox" name="opcionais" :value="opicional.tipo" v-model="opcionais">
                        <span>{{ opicional.tipo }}</span>
                    </div>
                </div>

                <!-- Escolha dos molhos -->
                <div class="input-form" id="molhos">
                    <label for="molhos" id="molhos-title">
                        Selecione os molhos:
                    </label>
                    <div class="checkbox" v-for="molho in molhos" :key="molho.id">
                        <input type="checkbox" name="molhos" :value="molho.tipo" v-model="molhosSelecionados">
                        <span>{{ molho.tipo }}</span>
                    </div>
                </div>

                <!-- Escolha dos queijos -->
                <div class="input-form" id="queijos">
                    <label for="queijo" id="queijos-title">
                        Escolha seus queijos:
                    </label>
                    <div class="checkbox" v-for="queijo in queijos" :key="queijo.id">
                        <input type="checkbox" name="queijo" :value="queijo.tipo" v-model="queijoSelecionado">
                        <span>{{ queijo.tipo }}</span>
                    </div>
                </div>

                <!-- Enviar -->
                <div class="input-form">
                    <input type="submit" class="submit-btn" value="Criar lanche!">
                </div>

            </form>
        </div>
    </div>
</template>

<script>
import Mensage from './Mensage.vue';

export default {
    name: 'Forms',
    components: {
        Mensage,
    },
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            molhos: null,
            queijos: null,
            nome: null,
            carne: null,
            opcionais: [],
            molhosSelecionados: [],
            queijoSelecionado: [],
            msg: null
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            console.log(data);

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;
            this.molhos = data.molhos;
            this.queijos = data.Queijos;
        },
        async createBurguer(e) {

            e.preventDefault();

            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                molhos: Array.from(this.molhosSelecionados),
                queijos: Array.from(this.queijoSelecionado),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            this.msg = `Pedido de ${res.nome} realizado com sucesso!`;

            setTimeout(() => this.msg = "", 3500);
            
            this.nome = "";
            this.carne = "";
            this.pao = "";
            this.opcionais = [];
            this.molhosSelecionados = [];
            this.queijoSelecionado = [];
        }
    },
    mounted() {
        this.getIngredientes()
    }
}
</script>

<style scoped>
#burguer-form {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.input-form {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 10px;
    color: #333;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
    font-size: 14px;
}

input,
select {
    padding: 10px;
    width: 100%;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 14px;
    transition: border-color 0.3s ease;
}

input:focus,
select:focus {
    border-color: #fcba03;
    outline: none;
}

#opcionais,
#molhos,
#queijos {
    flex-direction: row;
    flex-wrap: wrap;
    margin-top: 10px;
}

#opcionais-title,
#molhos-title,
#queijos-title {
    width: 100%;
    margin-bottom: 10px;
}

.checkbox {
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    align-items: center;
    width: 50%;
    margin-bottom: 15px;
}

.checkbox span,
.checkbox input {
    width: auto;
}

.checkbox span {
    margin-left: 8px;
    font-weight: bold;
    color: #555;
}

.submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 12px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s ease, color 0.3s ease;
    border-radius: 5px;
    width: 100%;
}

.submit-btn:hover {
    background-color: #fcba03;
    color: #222;
    border-color: #fcba03;
}

@media (max-width: 780px) {
    #burguer-form {
        max-width: 100%;
        padding: 15px;
    }

    .checkbox {
        width: 100%;
    }
}
</style>