<template>
  <v-container>
    <v-layout text-center wrap>
      <v-card>
        <pre> {{ arquivoConversa }} </pre>
          <h1>teste</h1>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  props: {
    arquivoConversa: File
  },

  data: () => ({
    arrayConversa: {}
    
  }),
  methods: {
    
    lerArquivoConversa(arquivoConversa){
      if (!arquivoConversa){ return false }

      let reader = new FileReader()

      reader.onload = (event) => {
        this.arrayConversa = event.target.result
        this.carregarChat(this.arrayConversa)
      }
      reader.readAsText(arquivoConversa)
    },
    carregarChat(){
      if (!this.arquivoConversa){ return false }
      console.log(this.arrayConversa)
    }

  },
  watch: {
    arquivoConversa: function(valor){
      this.lerArquivoConversa(valor)
    }
  }
};
</script>
