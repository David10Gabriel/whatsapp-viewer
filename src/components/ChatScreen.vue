<template>
  <v-container>
    <v-layout text-center wrap>
      <v-card>
        <pre> {{ objConversa }} </pre>
          <h1>teste</h1>
      </v-card>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  props: {
    objConversa: Object
  },

  data: () => ({
    
  }),
  methods: {
    carregarChat(){
      console.log("Teste carregar chat");
    }
  }
};
</script>
