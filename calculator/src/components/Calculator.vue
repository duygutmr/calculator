<template>
  <div class="calculator">
    <div class="current">{{answer}}</div>
    <div class="answer">{{logList + current}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn orange">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="times" class="btn orange">X</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn orange">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="plus" class="btn orange">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn orange">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      logList:'',
      previous: null,
      current: '',
      operator: null,
      operatorClicked: true,
      answer : '',
    }
 },
 methods : {
   clear() {
     this.current = '';
     this.previous = '';
     this.answer = '';
     this.logList = '';
     this.operatorClicked = false;
   },
   sign() {
     this.current = this.current * -1;
     
   },
   percent () {
     this.current = this.current / 100;
   },

  //  operatorClicked fonksiyonu +- gibi operatörlere basıldığında ekranın temizlenmesini söyler.
   append (number) {
     if(this.operatorClicked) {
       this.current = '';
       this.operatorClicked = false;
     }
     this.current = `${this.current}${number}`;
   },
   addtoLog(a) {
     if(this.operatorClicked == false) {
       this.logList += `${this.current}${a}`;
       this.current = '';
       this.operatorClicked = true;
     }
   },
    //  yazılan sayıların içinde nokta yoksa ekleme şartını kontrol ediyor.
    // bu yüzden yalnızca tek nokta yazılabilir.
   dot() {
    if (this.current.indexOf('.') === -1){
     this.append('.');
    }
   },
  //  operatörlere tıklanınca operatörü alıyor diğer sayının girilmesine izin veriyor
  setPrevious(){
      this.previous = eval(this.current);
      this.operatorClicked = true;
  },
   divide() {
     this.operator = (a, b) => a / b;
     this.addtoLog('/');
     this.setPrevious();
   },
   minus() {
     this.operator = (a, b) => a - b;
     this.addtoLog('-');
     this.setPrevious();
   },
   times() {
     this.operator = (a, b) => a * b;
     this.addtoLog('*');
     this.setPrevious();

   },
   plus() {
     this.operator = (a, b) => a + b;
     this.addtoLog('+');
     this.setPrevious();
   },
   equal() {
      if( this.operatorClicked == false) {
        this.answer = eval(this.logList + this.current);
      }
  }
} 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  font-size: 30px;
  display: grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px, auto);
}
.current{
  background-color: rgb(72, 80, 105);
  grid-column: 1 / 5;
  color: #fff;
}
.answer {
  grid-column: 1 / 5;
  background-color: rgb(72, 80, 105);
  color: #fff;
}
.zero {
  grid-column: 1 / 3;
}
.btn {
  background-color: #eee;
  cursor: pointer;
  border: 1px solid rgb(136, 129, 129);
}
.orange {
  background-color: orange;
}

</style>
