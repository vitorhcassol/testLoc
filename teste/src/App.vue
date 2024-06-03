<script>
export default {
  data(){
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
      var mensagemErro;

      switch (erro.code) {
        case 1:
          mensagemErro = "Permissão negada";
          break;
        case 2:
          mensagemErro = "Posição indisponível";
          break;
        case 3:
          mensagemErro = "Tempo limite expirado";
          break;
        default:
          mensagemErro = "Erro desconhecido (" + erro.code + ")";
      }

      alert("Erro de geolocalização: " + mensagemErro);
    },
  }
}

</script>

<template>
  <div>
    <button @click="obterLocalizacao">Teste</button>
    <p> {{ localizacao }} </p>
  </div>
</template>

<style scoped>
div {
  width: 100%;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

p {
  font-size: larger;
}
</style>
