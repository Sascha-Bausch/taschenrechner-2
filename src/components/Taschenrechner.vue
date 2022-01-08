<template>
  <div class="top">
    <!-- <h1>{{ msg }}</h1> -->
    <p>let's calculate</p>
  </div>
  <div class="taschenrechner">
    <div class="anzeige">{{ eingabe || "0" }}</div>
    <div @click="loeschen" class="taste">☠</div>
    <div @click="zeichen" class="taste-operator">+/-</div>
    <div @click="prozent" class="taste-operator">%</div>
    <div @click="geteilt" class="taste-operator">÷</div>
    <div @click="ziffer('7')" class="taste">7</div>
    <div @click="ziffer('8')" class="taste">8</div>
    <div @click="ziffer('9')" class="taste">9</div>
    <div @click="mal" class="taste-operator">x</div>
    <div @click="ziffer('4')" class="taste">4</div>
    <div @click="ziffer('5')" class="taste">5</div>
    <div @click="ziffer('6')" class="taste">6</div>
    <div @click="minus" class="taste-operator">-</div>
    <div @click="ziffer('1')" class="taste">1</div>
    <div @click="ziffer('2')" class="taste">2</div>
    <div @click="ziffer('3')" class="taste">3</div>
    <div @click="plus" class="taste-operator">+</div>
    <div @click="ziffer('0')" class="taste">0</div>
    <div @click="punkt" class="taste-operator">.</div>
    <div @click="quadrieren" class="taste-operator">x²</div>
    <div @click="wurzel" class="taste-operator">√</div>
    <div @click="ergebnis" class="taste-gleich">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      ersteEingabe: null,
      eingabe: "",
      operator: null,
      operatorKlick: false,
    };
  },
  methods: {
    loeschen() {
      this.eingabe = "";
    },
    zeichen() {
      this.eingabe =
        this.eingabe.charAt(0) === "-"
          ? this.eingabe.slice(1)
          : `-${this.eingabe}`;
    },
    prozent() {
      this.eingabe = `${parseFloat(this.eingabe) / 100}`;
    },
    quadrieren() {
      this.eingabe = `${Math.pow(this.eingabe, 2)}`;
    },
    wurzel() {
      this.eingabe = `${Math.sqrt(this.eingabe)}`;
    },
    ziffer(number) {
      if (this.operatorKlick) {
        this.eingabe = "";
        this.operatorKlick = false;
      }
      this.eingabe = `${this.eingabe}${number}`;
    },
    punkt() {
      if (this.eingabe.indexOf(".") === -1) {
        this.ziffer(".");
      }
    },
    merkeErsteEingabe() {
      this.ersteEingabe = this.eingabe;
      this.operatorKlick = true;
    },
    geteilt() {
      this.operator = (a, b) => b / a;
      this.merkeErsteEingabe();
    },
    mal() {
      this.operator = (a, b) => a * b;
      this.merkeErsteEingabe();
    },
    minus() {
      this.operator = (a, b) => b - a;
      this.merkeErsteEingabe();
    },
    plus() {
      this.operator = (a, b) => a + b;
      this.merkeErsteEingabe();
    },
    ergebnis() {
      this.eingabe = `${this.operator(
        parseFloat(this.eingabe),
        parseFloat(this.ersteEingabe)
      )}`;
      this.ersteEingabe = null;
    },
  },
};

/* export default {
  name: "Taschenrechner",
  props: {
    msg: String,
  },
}; */
</script>

<style scoped>
.taschenrechner {
  font-family: monospace;
  font-size: 35px;
  height: 250px;
  width: 250px;
  border: 3px solid rgb(57, 70, 70);
  border-radius: 5%;
  padding: 5%;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: minmax(50px, auto);
  background: lightgray;
  cursor: pointer;
}
.anzeige {
  grid-column: 1 / 5;
  background: lightcoral;
  border: 2px solid;
}
.taste-gleich {
  grid-column: 1/5;
  background-color: darkcyan;
  color: cornsilk;
  border: 2px solid;
  border-color: black;
}
.taste-operator {
  background-color: lightskyblue;
  border: 1px solid;
}
.taste {
  background-color: cornsilk;
  border: 1px solid;
}
</style>
