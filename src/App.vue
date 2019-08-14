<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      app
      clipped
    >
      <v-list dense>
        <v-list-item @click="$refs.inputChat.click()">
          <v-list-item-action>
            <v-icon>mdi-chat-outline</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title>Selecionar Conversa</v-list-item-title>
            <input v-show="false" id="inputChat" ref="inputChat" type="file" accept=".txt" @change="selecionarConversa">
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      clipped-left
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Application</v-toolbar-title>
    </v-app-bar>

    <v-content>
      <ChatScreen :objConversa = "conversaColetada">

      </ChatScreen>
    </v-content>

    <v-footer app>
      <span>&copy; 2019</span>
    </v-footer>

  <v-snackbar v-model="notificacao.estado" :color="notificacao.cor"> {{ notificacao.texto }} </v-snackbar>

  </v-app>
</template>

<script>
  import ChatScreen from './components/ChatScreen.vue'

  export default {
    components: { ChatScreen },
    props: {
      source: String,
    },
    data: () => ({
      drawer: null,
      conversaColetada: { texto: "Conversa coletada" },
      notificacao: {
        texto: null,
        cor: null,
        timeout: 5000,
        estado: false,
        enviar(textoNotificacao, corNotificacao){
            this.texto = textoNotificacao
            this.cor = corNotificacao
            this.estado = true
        }
      }
    }),
    created () {
      this.$vuetify.theme.dark = true
    },
    methods: {
      selecionarConversa(){
        this.conversaColetada = document.querySelector('#inputChat').files[0]
        console.log(this.conversaColetada);
        if(this.conversaColetada.type != 'text/plain'){
          this.notificacao.enviar("Seu naruto", "red")
        }
      }
    }
  }
</script>