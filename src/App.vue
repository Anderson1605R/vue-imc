<template>
  <main>
    <div>
      <h1>Calcule seu imc</h1>
      <label for="peso">Peso:</label>
      <input v-model="inputPeso" type="number" id="peso" />
      <label for="altura">Altura:</label>
      <input v-model="inputAltura" type="number" id="altura" />
      <button @click="calcular">Calcular</button>
    </div>
    <div class="res" v-if="resultado !== 'Aguardando'">
      <p>Seu IMC é: {{ resultado }}</p>
      <p>Sua classificação é: {{ classificacao }}</p>
    </div>
  </main>
</template>

<script>
export default {
  name: "App",
  components: {},

  data() {
    return {
      inputAltura: "",
      inputPeso: "",
      resultado: "Aguardando",
      classificacao: "",
    };
  },

  methods: {
    calcular() {
      const peso = Number(this.inputPeso);
      const altura = Number(this.inputAltura);
      const imc = (peso / (altura * altura)) * 10000;
      const resultado = imc.toFixed(2);
      this.resultado = resultado;

      if (resultado < 18.5) {
        this.classificacao = "Magreza";
      } else if (resultado >= 18.5 && resultado <= 24.99) {
        this.classificacao = "Normal";
      } else if (resultado >= 25 && resultado <= 29.99) {
        this.classificacao = "Sobrepeso";
      } else if (resultado >= 30 && resultado <= 39.99) {
        this.classificacao = "Obesidade";
      } else {
        this.classificacao = "Obesidade Grave";
      }
    },
  },
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}
main {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #242424;
  gap: 20px;
}
div {
  display: flex;
  flex-direction: column;
}
h1 {
  color: #ffff;
}
label {
  color: #ffff;
}
input {
  border-radius: 5px;
  outline: none;
}
button {
  padding: 5px;
  margin-top: 10px;
  background-color: rgb(180, 143, 214);
  border-radius: 5px;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: rgb(163, 114, 209);
}
.res {
  color: #ffff;
}
</style>
