<template>
  <v-container>
    <v-layout text-center wrap>
      <v-card>
        <!-- <pre> {{ arrayConversa }} </pre/> -->
        <v-flex v-for="mensagem in arrayConversa" :key="mensagem" >
          <v-tooltip top>
            <template v-slot:activator="{ on }">
              <v-chip color="darkgrey" pill v-on="on"> 
                <v-avatar left color="blue"> P </v-avatar> {{ mensagem }}
              </v-chip>
            </template>
            <span>Seu naruto</span>
          </v-tooltip>
        </v-flex>  
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
      this.arrayConversa = this.arrayConversa.split("\n")
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
