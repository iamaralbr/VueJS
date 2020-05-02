<template>
  <div class="componente">
    <h2>As Informações de Usuário</h2>
    <p>Vários detalhes...</p>
    <p>Nome do Usuário: <strong>{{ inverterNome }}</strong></p>
    <p>Idade do Usuário: <strong>{{ idadeUsu }}</strong></p>
    <button @click="reiniciarNome">Reiniciar Nome</button>
    <button @click="reiniciarFn">Reiniciar Nome (Callback)</button>
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
  // props: ['nome'],
  props: {
    // nome: [String, Array] // mais de um tipo
    nome: {
      type: String,
    //   required: true,
    //   default: () => {
      //       return Array(10).fill(0).join(',')
    //   }
      default: "Anônimo"
    },
    reiniciarFn: Function,
    idade: Number
  },
  computed: {
    inverterNome() {     
      return this.nome.split("").reverse().join("");
    }
  },
  methods: {
    reiniciarNome() {
      const antigo = this.nome
      const novo = 'Pedro'
      this.$emit('nomeMudou', {novo, antigo})      
    }
  },
  created() {
    barramento.quandoIdadeMudar(idade => {
      this.idadeUsu = idade
    })
  },
};
</script>

<style scoped>
.componente {
  flex: 1;
  background-color: #ec485f;
  color: #fff;
}
</style>
