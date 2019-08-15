<template>
  <v-container>
    <v-layout wrap>
      <v-flex xs12>
        <v-card>
          <v-card-text>
          <v-flex v-for="mensagem in arrayConversa" :key="mensagem.texto" :text-right="mensagem.texto.includes('David')">
            <v-tooltip top>
              <template v-slot:activator="{ on }">
                <v-chip v-if="mensagem.texto.includes('David')" color="darkgrey" pill v-on="on"> 
                  {{ mensagem.texto }}<v-avatar right color="blue">P</v-avatar>
                </v-chip>
                <v-chip v-else color="darkgrey" pill v-on="on"> 
                  <v-avatar left color="blue">P</v-avatar>{{ mensagem.texto }}
                </v-chip>
              </template>
              <span>{{ mensagem.remetente }}</span>
            </v-tooltip>
          </v-flex>  
          </v-card-text>  
        </v-card>
      </v-flex>  
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
      let arrayAuxiliar = []

      this.arrayConversa.forEach(mensagem => {
        arrayAuxiliar.push({
          texto: mensagem.split(":").slice(3, 10000).join(),
          data: mensagem.split("]")[0].replace("[", "")
          // remetente: mensagem.split(":")[2].split("]")[1],
        })
      });

      this.arrayConversa = arrayAuxiliar
    }

  },
  watch: {
    arquivoConversa: function(valor){
      this.lerArquivoConversa(valor)
    }
  }
};
</script>
