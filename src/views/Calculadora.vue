<script>
export default {
  data() {
    return {
      numero: 0,
      telaLimpa: true,
      parteArmazenada: "",
      operador: "",
      piscada: false
    }
  },
  methods: {
    // Botões: números, ponto, limpar e backspace

    getNumero(numero) {
      if (this.telaLimpa == true) {
        this.numero = "";
        this.numero = numero;
        this.telaLimpa = false;
      } else {
        this.numero = this.numero.concat(numero);
      }
      this.piscada = false;
    },

    limpar() {
      this.numero = 0;
      this.parteArmazenada = "";
      this.telaLimpa = true;
      this.piscada = false;
    },

    backspace() {
      this.numero = this.numero.substr(0, this.numero.length - 1);
    },

    // Botões: operadores

    usarOperador(operador) {
      if (this.parteArmazenada == "") {
        this.parteArmazenada = parseFloat(this.numero);
      } else {
        switch (this.operador) {
          case "+":
            this.parteArmazenada = parseFloat(this.parteArmazenada) + parseFloat(this.numero);
            break;
          case "-":
            this.parteArmazenada = parseFloat(this.parteArmazenada) - parseFloat(this.numero);
            break;
          case "*":
            this.parteArmazenada = parseFloat(this.parteArmazenada) * parseFloat(this.numero);
            break;
          case "/":
            this.parteArmazenada = parseFloat(this.parteArmazenada) / parseFloat(this.numero);
            break;
        }
      }
      this.operador = operador;
      this.telaLimpa = true;
      this.piscada = true;
    },

    // Botão: igual

    mostrarResultado() {
      switch (this.operador) {
        case "+":
          this.numero = (parseFloat(this.parteArmazenada) + parseFloat(this.numero)).toString();
          break;
        case "-":
          this.numero = (parseFloat(this.parteArmazenada) - parseFloat(this.numero)).toString();
          break;
        case "*":
          this.numero = (parseFloat(this.parteArmazenada) * parseFloat(this.numero)).toString();
          break;
        case "/":
          this.numero = (parseFloat(this.parteArmazenada) / parseFloat(this.numero)).toString();
          break;
      }
      this.parteArmazenada = "";
      this.telaLimpa = true;
      this.piscada = false;
    }
  }
}
</script>

<template>
  <main>
    <div id="calculadora">
      <input type="text" :class="{ 'tela': piscada }" :value="numero" readonly>

      <div class="linha">
        <button type="button" style="visibility: hidden"></button>
        <button type="button" style="visibility: hidden"></button>
        <button type="button" class="btn btn-light" @click="limpar()">ce</button>
        <button type="button" style="font-size: 1.25rem" class="btn btn-light" @click="backspace()">&lt</button>
      </div>
      <div class="linha">
        <button type="button" class="btn btn-light" ref="numero7" value="7"
          @click="getNumero($refs.numero7.value)">7</button>
        <button type="button" class="btn btn-light" ref="numero8" value="8"
          @click="getNumero($refs.numero8.value)">8</button>
        <button type="button" class="btn btn-light" ref="numero9" value="9"
          @click="getNumero($refs.numero9.value)">9</button>
        <button type="button" class="btn btn-light" ref="divisao" value="/"
          @click="usarOperador($refs.divisao.value)">÷</button>
      </div>
      <div class="linha">
        <button type="button" class="btn btn-light" ref="numero4" value="4"
          @click="getNumero($refs.numero4.value)">4</button>
        <button type="button" class="btn btn-light" ref="numero5" value="5"
          @click="getNumero($refs.numero5.value)">5</button>
        <button type="button" class="btn btn-light" ref="numero6" value="6"
          @click="getNumero($refs.numero6.value)">6</button>
        <button type="button" class="btn btn-light" ref="multiplicacao" value="*"
          @click="usarOperador($refs.multiplicacao.value)">x</button>
      </div>
      <div class="linha">
        <button type="button" class="btn btn-light" ref="numero1" value="1"
          @click="getNumero($refs.numero1.value)">1</button>
        <button type="button" class="btn btn-light" ref="numero2" value="2"
          @click="getNumero($refs.numero2.value)">2</button>
        <button type="button" class="btn btn-light" ref="numero3" value="3"
          @click="getNumero($refs.numero3.value)">3</button>
        <button type="button" class="btn btn-light" ref="subtracao" value="-"
          @click="usarOperador($refs.subtracao.value)">-</button>
      </div>
      <div class="linha">
        <button type="button" class="btn btn-light" ref="numero0" value="0"
          @click="getNumero($refs.numero0.value)">0</button>
        <button type="button" class="btn btn-light" ref="ponto" value="." @click="getNumero($refs.ponto.value)">.</button>
        <button type=" button" class="btn btn-light" @click="mostrarResultado()">=</button>
        <button type="button" class="btn btn-light" ref="soma" value="+"
          @click="usarOperador($refs.soma.value)">+</button>
      </div>
    </div>
  </main>
</template>

<style scoped>
#calculadora {
  height: 28rem;
  width: 20rem;
  background-color: rgb(129, 129, 129);
  padding: 2rem;
  border-radius: 0.3rem;
}

.tela {
  animation-duration: 0.1s;
  animation-name: piscada;
}

@keyframes piscada {
  from {
    color: black;
  }

  50% {
    color: white;
  }

  to {
    color: black;
  }
}

div>input {
  height: 2.75rem;
  width: 100%;
  font-size: 1.5rem;
  font-weight: 500;
  border-radius: 0.3rem;
  padding-left: 0.5rem;
  padding-right: 0.5rem;
}

#calculadora button {
  height: 2.75rem;
  width: 2.75rem;
  border: 1px solid black;
  border-radius: 0.3rem;
  margin-top: 1.3rem;
  font-size: 1.5rem;
  font-weight: 500;
}

.linha {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
</style>
