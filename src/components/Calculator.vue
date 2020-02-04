<template>

  <div class="calculator">
<div class="display">{{current || '0'}}</div>
<div @click="clear" class="btn"> C </div>
<div @click="sign" class="btn"> +/- </div>
<div @click="percent" class="btn"> % </div>
<div @click="bagi" class="btn operator"> ÷ </div>
<div @click="append('7')" class="btn"> 7 </div>
<div @click="append('8')" class="btn"> 8 </div>
<div @click="append('9')" class="btn"> 9 </div>
<div @click="kali" class="btn operator"> x </div>
<div @click="append('4')" class="btn"> 4 </div>
<div @click="append('5')" class="btn"> 5 </div>
<div @click="append('6')" class="btn"> 6 </div>
<div @click="kurang" class="btn operator"> - </div>
<div @click="append('1')" class="btn"> 1 </div>
<div @click="append('2')" class="btn"> 2 </div>
<div @click="append('3')" class="btn"> 3 </div>
<div @click="tambah" class="btn operator"> + </div>
<div @click="append('0')" class="btn zero"> 0 </div>
<div @click="dot" class="btn"> . </div>
<div @click="hasil" class="btn operator"> = </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear () {
      this.current = ''
    },
    sign () {
      this.current = this.current.charAt(0) === '-'
        ? this.current.slice(1) : `-${this.current}`
    },
    percent () {
      this.current = `${parseFloat(this.current) / 100}`
    },
    append (number) {
      if (this.operatorClicked) {
        this.current = ''
        this.operatorClicked = false
      }
      this.current = `${this.current}${number}`
    },
    dot () {
      if (this.current.indexOf('.') === -1) {
        this.append('.')
      }
    },
    setPrevious () {
      this.previous = this.current
      this.operatorClicked = true
    },
    bagi () {
      this.operator = (a, b) => b / a
      this.setPrevious()
    },
    kali () {
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    kurang () {
      this.operator = (a, b) => b - a
      this.setPrevious()
    },
    tambah () {
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    hasil () {
      this.current = `${this.operator(parseFloat(this.current), parseFloat(this.previous))}`
      this.previous = null
    }
  }
}
</script>

<style scoped>
main {
  background-color:black
}

.calculator {
  margin: 0 auto;
  width: 700px;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  }
.display{
  grid-column: 1 / 5;
  background: chocolate;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color:#f2f2f2;
  border: 1px solid #999;
}
.operator {
  background-color: rebeccapurple;
  color: white;
}
</style>
