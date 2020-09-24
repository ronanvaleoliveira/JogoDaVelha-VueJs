<template>
  <div class="">
    <div class="container header">
      <div class="row justify-content-md-center">
        <div class="col col-lg-2">
          <button class="resetar2" v-on:click="novoJogo()">Novo jogo</button>
        </div>
        <div class="col col-lg-4">
          <label v-if="!partidaEncerrada"> Jogador: '{{ jogador }}'</label>
          <label v-if="partidaEncerrada"
            >O jogador '{{ vencedor }}' ganhou !</label
          >
        </div>
      </div>
    </div>

    <div class="game">
      <div class="row">
        <button
          class="bntTabuleiro btn00"
          v-on:click="jogar('00')"
          :disabled="partidaEncerrada || p00 == 'X' || p00 == 'O'"
        >
          {{ p00 }}
        </button>
        <button
          class="bntTabuleiro btn01"
          v-on:click="jogar('01')"
          :disabled="partidaEncerrada || p01 == 'X' || p01 == 'O'"
        >
          {{ p01 }}
        </button>
        <button
          class="bntTabuleiro btn02"
          v-on:click="jogar('02')"
          :disabled="partidaEncerrada || p02 == 'X' || p02 == 'O'"
        >
          {{ p02 }}
        </button>

        <button
          class="bntTabuleiro btn10"
          v-on:click="jogar('10')"
          :disabled="partidaEncerrada || p10 == 'X' || p10 == 'O'"
        >
          {{ p10 }}
        </button>
        <button
          class="bntTabuleiro btn11"
          v-on:click="jogar('11')"
          :disabled="partidaEncerrada || p11 == 'X' || p11 == 'O'"
        >
          {{ p11 }}
        </button>
        <button
          class="bntTabuleiro btn12"
          v-on:click="jogar('12')"
          :disabled="partidaEncerrada || p12 == 'X' || p12 == 'O'"
        >
          {{ p12 }}
        </button>

        <button
          class="bntTabuleiro btn20"
          v-on:click="jogar('20')"
          :disabled="partidaEncerrada || p20 == 'X' || p20 == 'O'"
        >
          {{ p20 }}
        </button>
        <button
          class="bntTabuleiro btn21"
          v-on:click="jogar('21')"
          :disabled="partidaEncerrada || p21 == 'X' || p21 == 'O'"
        >
          {{ p21 }}
        </button>
        <button
          class="bntTabuleiro btn22"
          v-on:click="jogar('22')"
          :disabled="partidaEncerrada || p22 == 'X' || p22 == 'O'"
        >
          {{ p22 }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import VueToast from "vue-toast-notification";
import "vue-toast-notification/dist/theme-default.css";
Vue.use(VueToast);
export default {
  data() {
    return {
      partidaEncerrada: false,
      vencedor: "",
      jogador: "X",
      p00: "",
      p01: "",
      p02: "",
      p10: "",
      p11: "",
      p12: "",
      p20: "",
      p21: "",
      p22: "",
    };
  },
  methods: {
    novoJogo() {
      this.p00 = "";
      this.p01 = "";
      this.p02 = "";
      this.p10 = "";
      this.p11 = "";
      this.p12 = "";
      this.p20 = "";
      this.p21 = "";
      this.p22 = "";
      this.partidaEncerrada = false;
      Vue.$toast.clear();
    },
    pararJogo() {
      this.partidaEncerrada = true;

      Vue.$toast.success("O jogador '" + this.vencedor + "' ganhou !", {
        position: "top-right",
        duration: 5000,
      });
    },
    trocarJogador() {
      this.jogador = this.jogador === "X" ? "O" : "X";
    },
    jogar(position) {
      //debugger; // eslint-disable-line no-debugger
      switch (position) {
        case "00":
          this.p00 = this.jogador;
          break;
        case "01":
          this.p01 = this.jogador;
          break;
        case "02":
          this.p02 = this.jogador;
          break;

        case "10":
          this.p10 = this.jogador;
          break;
        case "11":
          this.p11 = this.jogador;
          break;
        case "12":
          this.p12 = this.jogador;
          break;

        case "20":
          this.p20 = this.jogador;
          break;
        case "21":
          this.p21 = this.jogador;
          break;
        case "22":
          this.p22 = this.jogador;
          break;
        default:
          break;
      }

      this.trocarJogador();
      this.verificarVencedor();
    },

    verificarVencedor() {
      this.vencedorHorizontal();
      this.vencedorVertical();
      this.vencedorDiagonal();
    },
    vencedorHorizontal() {
      //debugger; // eslint-disable-line no-debugger
      let combinacao = "";

      combinacao = this.p00 + this.p01 + this.p02;
      this.verificaCombinacao(combinacao);

      combinacao = this.p10 + this.p11 + this.p12;
      this.verificaCombinacao(combinacao);

      combinacao = this.p20 + this.p21 + this.p22;
      this.verificaCombinacao(combinacao);
    },
    vencedorVertical() {
      let combinacao = "";

      combinacao = this.p00 + this.p10 + this.p20;
      this.verificaCombinacao(combinacao);

      combinacao = this.p01 + this.p11 + this.p21;
      this.verificaCombinacao(combinacao);

      combinacao = this.p02 + this.p12 + this.p22;
      this.verificaCombinacao(combinacao);
    },
    vencedorDiagonal() {
      let combinacao = "";

      combinacao = this.p00 + this.p11 + this.p22;
      this.verificaCombinacao(combinacao);

      combinacao = this.p02 + this.p11 + this.p20;
      this.verificaCombinacao(combinacao);
    },

    verificaCombinacao(combinacao) {
      if (combinacao == "XXX") {
        this.vencedor = "X";
        this.pararJogo();
      } else if (combinacao == "OOO") {
        this.vencedor = "O";
        this.pararJogo();
      }
    },
  },
};
</script>

<style>
body {
  background-color: rgb(20, 189, 172);
}
.header {
  margin-top: 20px;
}
.game {
  position: relative;
  display: block;
  margin: 5% auto;
  width: 450px;
  padding: 5px;
  text-align: center;
}

.bntTabuleiro {
  width: 140px;
  height: 140px;
  border: 5px solid rgb(13, 161, 146);
  font-size: 80px;
  /* color: transparent; */
  margin-right: -4px;
  background: none;
  cursor: pointer;
}

.activedX {
  color: #666;
}
.activedO {
  color: #fff;
}

label {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 30px;
  font-weight: bold;
  color: rgb(13, 161, 146);
}
.resetar {
  position: absolute;
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #eee;
  border: none;
  color: rgb(13, 161, 146);
  font-size: 20px;
  cursor: pointer;
}
.resetar2 {
  bottom: 0;
  width: 100%;
  height: 50px;
  background-color: #eee;
  border: none;
  color: rgb(13, 161, 146);
  font-size: 20px;
  cursor: pointer;
}
.btn00 {
  border-left: transparent;
  border-top: transparent;
}
.btn01 {
  border-top: transparent;
}
.btn02 {
  border-right: transparent;
  border-top: transparent;
}
.btn10 {
  border-top: transparent;
  border-left: transparent;
  border-bottom: transparent;
}
.btn11 {
  border-top: transparent;
  border-bottom: transparent;
}
.btn12 {
  border-right: transparent;
  border-top: transparent;
  border-bottom: transparent;
}
.btn20 {
  border-left: transparent;
  border-bottom: transparent;
}
.btn21 {
  border-bottom: transparent;
}
.btn22 {
  border-right: transparent;
  border-bottom: transparent;
}
</style>