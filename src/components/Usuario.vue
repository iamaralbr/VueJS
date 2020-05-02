<template>
    <div class="container">
        <h1>Componente Usuário</h1>
        <p>Esse é um componente muito legal!</p>
        <p>Nome é <strong>{{ nome }}</strong></p>
        <p>
        <button @click="idade -= 1">-</button>
        Idade é <strong>{{ idade }}</strong>
        <button @click="idade += 1">+</button>
        </p>
        <button @click="alterarNome">Alterar Nome</button>
        <hr>
        <div class="componentes">
            <app-usuario-info 
              :nome="nome" 
              :idade="idade"
              @nomeMudou="nome = $event.novo"
              :reiniciarFn="reiniciarNome" />
            <app-usuario-editar 
              :nome="nome"
              :idade="idade"
              :reiniciarIdadeFn="reiniciarIdade" />
              <!-- @idadeMudou="idade = $event" /> -->
        </div>
    </div>
</template>

<script>
import AppUsuarioInfo from './UsuarioInfo'
import AppUsuarioEditar from './UsuarioEditar'
import barramento from '@/barramento'

export default {
    components: { AppUsuarioInfo, AppUsuarioEditar },
    data() {
        return {
            nome: 'Pedro',
            idade: 21
        }
    },
    methods: {
        alterarNome() {
            this.nome = 'Ana'
        },
        reiniciarNome() {
            this.nome = 'Pedro'
        },
        reiniciarIdade() {
            barramento.alterarIdade(this.idade)
        }
    }
}
</script>

<style scoped>
    .container {
        background-color: #27363b;
        color: #fff;
        padding: 10px;
    }

    .container hr {
        margin: 20px 10px;
    }

    .componentes {
        display: flex;
    }

    .componentes > * {
        margin: 10px;
    }
</style>
