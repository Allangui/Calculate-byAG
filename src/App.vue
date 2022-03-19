<template>
  <main>
    <header>
      <span class="calc">calc</span>
      <span class="theme">theme</span>
      <div class="gridForToggle">
        <span class="for1">1</span>
        <span class="for2">2</span>
        <span class="for3">3</span>
        <input type="range" class="toggleTheme" min="1" max="3" v-model="toggleValue" @change="toggleTheme(toggleValue)">
      </div>
    </header>
    <div class="result" >{{ result }}</div>
    <div class="keyboard">
      <div class="div1" @click="calcul(7)">7</div>
      <div class="div2" @click="calcul(8)">8</div>
      <div class="div3" @click="calcul(9)">9</div>
      <div class="div4" @click="del()">del</div>
      <div class="div5" @click="calcul(4)">4</div>
      <div class="div6" @click="calcul(5)">5</div>
      <div class="div7" @click="calcul(6)">6</div>
      <div class="div8" @click="action('+')">+</div>
      <div class="div9" @click="calcul(1)">1</div>
      <div class="div10" @click="calcul(2)">2</div>
      <div class="div11" @click="calcul(3)">3</div>
      <div class="div12" @click="action('-')">-</div>
      <div class="div13" @click="calcul('.')">.</div>
      <div class="div14" @click="calcul(0)">0</div>
      <div class="div15" @click="action('/')">/</div>
      <div class="div16" @click="action('*')">x</div>
      <div class="div17" @click="reset()">reset</div>
      <div class="div18" @click="equal()" >=</div>
    </div>
  </main>
</template>

<script>
  export default {
    data() {
      return {
        toggleValue: 1,
        result:'0',
        resultTemp:'',
      }
    },
    methods: {
      calcul(value){
        if ((this.result=='0' && value!= '.') || this.result=='NaN'){
        this.result = this.result.replace(this.result,value)
        }
        else if((this.result.substr(-1) == '-')||
        (this.result.substr(-1) == '+')||
        (this.result.substr(-1) == '*')||
        (this.result.substr(-1) == '/')
        ){
          if(value=='.'){
            this.resultTemp = this.result
            this.result = '0' + value.toString(10)
          }else{
            this.resultTemp = this.result
            this.result = value.toString(10)
          }
        }
        else{
          this.result += value
        }
      },
      action(operate){
        if((this.result.substr(-1) == '-')||
        (this.result.substr(-1) == '+')||
        (this.result.substr(-1) == '*')||
        (this.result.substr(-1) == '/')
        ){
          this.result = this.result.replace(this.result.substr(-1),operate)
        }else if(this.resultTemp){
          this.equal(operate)
          
        }else if(this.result=='NaN'){
          this.result='0'
        }
        else{
          this.result += operate
        }
        
      },
      del(){
        this.result = this.result.substring(0,this.result.length-1)
        if(this.result.length== 0){
          this.result = '0'
        }
      },
      reset(){
        this.result = '0'
        this.resultTemp= ''
      },
      equal(operate){
          switch(this.resultTemp.substr(-1)){
            case '+':
              this.result = parseFloat(this.result,10)
              this.resultTemp = parseFloat(this.resultTemp,10)
              this.result+= this.resultTemp
              this.result = Math.round(this.result*10000)/10000
              if(operate){
                this.result = this.result.toString(10) + operate
              }else{
                this.result = this.result.toString(10)
                this.resultTemp=''
              }
              break
            case '-':
              this.result = parseFloat(this.result)
              this.resultTemp = parseFloat(this.resultTemp)
              this.result = this.resultTemp - this.result
              this.result = Math.round(this.result*10000)/10000
              if(operate){
                this.result = this.result.toString(10) + operate
              }else{
                this.result = this.result.toString(10)
                this.resultTemp=''
              }              
              break
              case '*':
              this.result = parseFloat(this.result)
              this.resultTemp = parseFloat(this.resultTemp)
              this.result *= this.resultTemp
              this.result = Math.round(this.result*10000)/10000
              if(operate){
                this.result = this.result.toString(10) + operate
              }else{
                this.result = this.result.toString(10)
                this.resultTemp=''
              }              
              break
              case '/':
              this.result = parseFloat(this.result)
              this.resultTemp = parseFloat(this.resultTemp)
              this.result = this.resultTemp / this.result
              this.result = Math.round(this.result*10000)/10000
              if(operate){
                this.result = this.result.toString(10) + operate
              }else{
                this.result = this.result.toString(10)
                this.resultTemp=''
              }              
              break              
          }
      },
      toggleTheme(togVal) {
        localStorage.setItem('toggleValue',togVal)
        if(togVal==1){
        document.documentElement.style.setProperty('--mainBg', 'hsl(222, 26%, 31%)')
        document.documentElement.style.setProperty('--toggKeyBg', 'hsl(223, 31%, 20%)')
        document.documentElement.style.setProperty('--screenBg', 'hsl(224, 36%, 15%)')
        document.documentElement.style.setProperty('--keyBg', 'hsl(30, 25%, 89%)')
        document.documentElement.style.setProperty('--keyShadow', 'hsl(28, 16%, 65%)')
        document.documentElement.style.setProperty('--keyResultTogg', 'hsl(6, 63%, 50%)')
        document.documentElement.style.setProperty('--keyResultShadow', 'hsl(6, 70%, 34%)')
        document.documentElement.style.setProperty('--keyResDelBg', 'hsl(225, 21%, 49%)')
        document.documentElement.style.setProperty('--keyResDelShadow', 'hsl(224, 28%, 35%)')
        document.documentElement.style.setProperty('--textColor1', 'hsl(221, 14%, 31%)')
        document.documentElement.style.setProperty('--textColor2', 'white')
        document.documentElement.style.setProperty('--textColor3', 'white')
        document.documentElement.style.setProperty('--textColor4', 'white')
        }else if(togVal==2){
        document.documentElement.style.setProperty('--mainBg', 'hsl(0, 0%, 90%)')
        document.documentElement.style.setProperty('--toggKeyBg', 'hsl(0, 5%, 81%)')
        document.documentElement.style.setProperty('--screenBg', 'hsl(0, 0%, 93%)')
        document.documentElement.style.setProperty('--keyBg', 'hsl(45, 7%, 89%)')
        document.documentElement.style.setProperty('--keyShadow', 'hsl(35, 11%, 61%)')
        document.documentElement.style.setProperty('--keyResultTogg', 'hsl(25, 98%, 40%)')
        document.documentElement.style.setProperty('--keyResultShadow', 'hsl(25, 99%, 27%)')
        document.documentElement.style.setProperty('--keyResDelBg', 'hsl(185, 42%, 37%)')
        document.documentElement.style.setProperty('--keyResDelShadow', 'hsl(185, 58%, 25%)')
        document.documentElement.style.setProperty('--textColor1', 'hsl(60, 10%, 19%)')
        document.documentElement.style.setProperty('--textColor2', 'hsl(60, 10%, 19%)')
        document.documentElement.style.setProperty('--textColor3', 'white')
        document.documentElement.style.setProperty('--textColor4', 'white')
        }else{
        document.documentElement.style.setProperty('--mainBg', 'hsl(268, 75%, 9%)')
        document.documentElement.style.setProperty('--toggKeyBg', 'hsl(268, 71%, 12%)')
        document.documentElement.style.setProperty('--screenBg', 'hsl(268, 71%, 12%)')
        document.documentElement.style.setProperty('--keyBg', 'hsl(268, 47%, 21%)')
        document.documentElement.style.setProperty('--keyShadow', 'hsl(290, 70%, 36%)')
        document.documentElement.style.setProperty('--keyResultTogg', 'hsl(176, 100%, 44%)')
        document.documentElement.style.setProperty('--keyResultShadow', 'hsl(177, 92%, 70%)')
        document.documentElement.style.setProperty('--keyResDelBg', 'hsl(281, 89%, 26%)')
        document.documentElement.style.setProperty('--keyResDelShadow', 'hsl(285, 91%, 52%)')
        document.documentElement.style.setProperty('--textColor1', 'hsl(52, 100%, 62%)')
        document.documentElement.style.setProperty('--textColor2', 'hsl(52, 100%, 62%)')
        document.documentElement.style.setProperty('--textColor3', 'white')
        document.documentElement.style.setProperty('--textColor4', 'hsl(198, 20%, 13%)')
        }
      }
    },
    mounted () {
      if(localStorage.getItem('toggleValue')){
        this.toggleValue = localStorage.getItem('toggleValue')
        this.toggleTheme(localStorage.getItem('toggleValue'))
      }else{
        this.toggleTheme(this.toggleValue)
      }
    },
  }
</script>

<style scoped lang="scss">
main{
  width:90vw;
  max-width: 450px;
  margin:20px auto;
  padding: 5px;
  display: flex;
  flex-direction: column;
  row-gap: 20px;

  header{
    width:100%;
    min-width:325px;
    color:var(--textColor2);
    display: grid;
    grid-template-columns:  auto 1fr auto;
    grid-template-rows:  repeat(2 auto);
    padding: 5px 0;
    align-items: center;
    .calc{
      grid-column:1 ;
      grid-row: span 2;
    }
    .theme{
      font-size: .9rem;
      line-height: 1.2rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      align-self: end;
      justify-self: end;
      grid-column: 2;
      grid-row: 2;
      margin-right:30px;
    }
    .gridForToggle{
      grid-column: 3;
      grid-row: span 2;
      display: grid;
      justify-self: end;
      grid-template-columns: auto auto auto;
      grid-template-rows: auto auto;
      font-size: .8rem;
      width:70px;
      .for1,.for2,.for3{
        justify-self: center;
        grid-row: 1;
        line-height: 1.4rem;
      }
      .for1{
        grid-column: 1;
      }
      .for2{
        grid-column: 2;
      }
      .for3{
        grid-column: 3;
      }
      input{
        grid-column: span 3;
        grid-row: 2;
        background: transparent;
      }
      input[type=range] {
        -webkit-appearance: none;
        width: 100%;
      }
      input[type=range]:focus {
        outline: none;
      }
      input[type=range]::-webkit-slider-runnable-track {
        padding:0 5px;
        width: 100%;
        height: 30px;
        cursor: pointer;
        animate: 0.2s;
        background: var(--toggKeyBg);
        border-radius: 50px;
      }
      input[type=range]::-webkit-slider-thumb {
        height: 20px;
        width: 20px;
        border-radius: 50px;
        background: var(--keyResultTogg);
        cursor: pointer;
        -webkit-appearance: none;
        margin-top: 5px;
      }
      input[type=range]:focus::-webkit-slider-runnable-track {
        background: var(--toggKeyBg);
      }
      input[type=range]::-moz-range-track {
        width: 100%;
        height: 30px;
        padding:0 5px;
        cursor: pointer;
        animate: 0.2s;
        background:var(--toggKeyBg);
        border-radius: 50px;
      }
      input[type=range]::-moz-range-thumb {
        height: 20px;
        width: 20px;
        border-radius: 50px;
        background: var(--keyResultTogg);
        cursor: pointer;
      }
      input[type=range]::-ms-track {
        width: 100%;
        height: 30px;
        padding:0 5px;
        cursor: pointer;
        animate: 0.2s;
        background: transparent;
        border-color: transparent;
        color: transparent;
      }
      input[type=range]::-ms-fill-lower {
        background: var(--toggKeyBg);
        border-radius: 100px;
      }
      input[type=range]::-ms-fill-upper {
        background: var(--toggKeyBg);
        border-radius: 100px;
      }
      input[type=range]::-ms-thumb {
        height: 20px;
        width: 20px;
        border-radius: 50px;
        background: var(--keyResultTogg);
        cursor: pointer;
      }
      input[type=range]:focus::-ms-fill-lower {
        background: var(--toggKeyBg);
      }
      input[type=range]:focus::-ms-fill-upper {
        background: var(--toggKeyBg);
      }
    }
  }
  .result{
    background-color: var(--screenBg);
    width:100%;
    min-width:325px;
    padding:25px 20px;
    border-radius: 10px;
    display: flex;
    justify-content:flex-end ;
    align-items: center;
    align-content: center;
    color: var(--textColor2);
    overflow: hidden;
    margin:auto;
    
  }
  .keyboard{
    width:100%;
    min-width: 325px;
    background-color:var(--toggKeyBg);
    border-radius: 10px;
    margin:auto;
    padding:20px;
    display: grid;
    grid-template-columns: repeat(4, auto);
    grid-template-rows: repeat(5, 63px);
    grid-column-gap: 15px;
    grid-row-gap: 15px;
    .div1 ,.div2 , .div3 , .div5 , .div6 , .div7 , .div8 , .div9 , .div10 , .div11 , .div12 , .div13 , .div14 , .div15 , .div16{
      background-color: var(--keyBg);
      color:var(--textColor1);
      display:flex;
      justify-content:center;
      align-items: center;
      border-radius: 5px;
      border-bottom: 3px solid var(--keyShadow);
      cursor: pointer;
    } 
    .div4,.div17{
      background-color: var(--keyResDelBg);
      color:var(--textColor3);
      text-transform: uppercase;
      font-size: 1rem;
      letter-spacing: .5px;
      border-radius: 5px;
      border-bottom: 3px solid var(--keyResDelShadow);
      display:flex;
      justify-content:center;
      align-items: center;
      cursor: pointer;
    } 
    .div1 { grid-area: 1 / 1 / 2 / 2; }
    .div2 { grid-area: 1 / 2 / 2 / 3; }
    .div3 { grid-area: 1 / 3 / 2 / 4; }
    .div4 { grid-area: 1 / 4 / 2 / 5; }
    .div5 { grid-area: 2 / 1 / 3 / 2; }
    .div6 { grid-area: 2 / 2 / 3 / 3; }
    .div7 { grid-area: 2 / 3 / 3 / 4; }
    .div8 { grid-area: 2 / 4 / 3 / 5; }
    .div9 { grid-area: 3 / 1 / 4 / 2; }
    .div10 { grid-area: 3 / 2 / 4 / 3; }
    .div11 { grid-area: 3 / 3 / 4 / 4; }
    .div12 { grid-area: 3 / 4 / 4 / 5; }
    .div13 { grid-area: 4 / 1 / 5 / 2; }
    .div14 { grid-area: 4 / 2 / 5 / 3; }
    .div15 { grid-area: 4 / 3 / 5 / 4; }
    .div16 { grid-area: 4 / 4 / 5 / 5; }
    .div17 { grid-area: 5 / 1 / 6 / 3; }
    .div18 { 
    grid-area: 5 / 3 / 6 / 5;
    background-color: var(--keyResultTogg);
    color:var(--textColor4);
    font-size: 1.2rem;
    border-radius: 5px;
    border-bottom: 3px solid var(--keyResultShadow);
    display:flex;
    justify-content:center;
    align-items: center;
    cursor: pointer;
    }
  }
}
</style>

<style lang="scss" >

body{
  background-color: var(--mainBg);
  font-family: 'Spartan', sans-serif;
  font-weight: 700;
  font-size: 32px;
}
</style>