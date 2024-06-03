<template>
  <div id="app">
    <button @click="obterLocalizacao">mostrar localizacao</button>
    <p>{{ localizacao }}</p>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
      return {
          localizacao: ''
      }
  },

  methods: {
    obterLocalizacao() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.mostrarLocalizacao, this.mostrarErro);
      } else {
        alert("Seu navegador não suporta geolocalização.");
      }
    },

    mostrarLocalizacao(posicao) {
      var latitude = posicao.coords.latitude;
      var longitude = posicao.coords.longitude;

      this.localizacao = "Sua localização atual é: " + latitude + ", " + longitude;
    },

  mostrarErro(erro) {
    switch (erro.code) {
      case 1:
      this.localizacao = "Permissão negada";
      break;
      case 2:
      this.localizacao = "Posição indisponível";
      break;
      case 3:
      this.localizacao = "Tempo limite expirado";
      break;
      default:
      this.localizacao = "Erro desconhecido (" + erro.code + ")";
    }
    }
  }
};
</script>

<style scoped>
#app {
  font-family: sans-serif;
  text-align: center;
}

p {
  font-size: larger;
}
</style>
