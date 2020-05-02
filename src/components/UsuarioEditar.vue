<template>
    <div class="componente">
        <h2>Alterar os Dados de Usuário</h2>
        <p>Edite as informações</p>
        <p>Nome do Usuário: <strong>{{ nome }}</strong></p>
        <p>Idade do Usuário: <strong>{{ idadeUsu }}</strong></p>
        <button @click="alterarIdade">Alterar Idade</button>
        <button @click="reiniciarIdadeFn">Idade Original (Callback)</button>
    </div>
</template>

<script>
import barramento from '@/barramento'

export default {
  data() {
    return {
      idadeUsu: this.idade
    }
  },
  props: {
    nome: String,
    idade: Number,
    reiniciarIdadeFn: Function
  },
  methods: {
    alterarIdade() {
      this.idadeUsu += 1
      barramento.alterarIdade(this.idadeUsu)
    }
  },
  created() {
    barramento.quandoIdadeMudar(idade => {
      this.idadeUsu = idade
    })
  }
}
</script>

<style scoped>
    .componente {
        flex: 1;
        background-color: #98b99a;
        color: #fff;
    }
</style>
