<template>
  <div id="app">
    <h1>Formulário de alunos</h1>  
          <form @submit.prevent="salvar()">
              <label for="nome">Nome</label>
              <input type="text" id="nome" v-model="nome"  size="30" required autofocus><br/>
              <label for="nota1">Nota 1:</label>
              <input type="number" id="nota1" v-model="nota1" required><br/>
              <label for="nota2">Nota 2:</label>
              <input type="number" id="nota2" v-model="nota2" required><br/>
              <label for="nota3">Nota 3:</label>
              <input type="number" id="nota3" v-model="nota3" required><br/>
              <label for="mediaExercicio">Nota Media Exercicios:</label>
              <input type="number" id="mediaExercicio" v-model="mediaExercicio" required><br/>
              <input type="submit" value="Salvar"/>
              <input type="button" value="Cancelar" @click="cancelarFormulario"/>
              <br/>
          </form>

          <table>
            <tr>
              <th>Nome</th>
              <th>Status</th>
            </tr>
            <tr v-for="p in Alunos" :key="p.id" >
                <td>{{ p.nome }}</td>
                <td>{{ p.status }}</td>
            </tr>
          </table>
  </div>
</template>

<script>
export default {

  data(){
    return {
      nome: null,
      nota1: null,
      nota2: null,
      nota3: null,
      mediaExercicio: null,
      media:null,
      status: null,
      Alunos:[]
    }
  },

methods:{
  cancelarFormulario() {
      this.nome = null
      this.nota1 = null
      this.nota2 = null
      this.nota3 = null
      this.mediaExercicio = null
    },
    salvar() {
      let aluno = {
        nome: this.nome,
        nota1: this.nota1,
        nota2: this.nota2,
        nota3: this.nota3,
        mediaExercicio: this.mediaExercicio,
        media: (parseFloat(this.nota1) + parseFloat(this.nota2) * 2 + parseFloat(this.nota3) * 3 + parseFloat(this.mediaExercicio))/7 
      }
      console.log(aluno.media)
      if(aluno.media >= 7){
        this.status = 'Aprovado'
      } else{
        this.status = 'Reprovado'
      }
      aluno.status = this.status
      this.Alunos.push(aluno)
    },

},

computed:{
  totalSalvo() {
      return this.Alunos.length;
    }
}

}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.Aprovado{
  background-color: blue;
}

.Reprovado{
  background-color: red;
}

table, th, td {
  border: 1px solid black;
}
</style>
