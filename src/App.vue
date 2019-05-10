<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
      <input ref="input1" v-model="input1" placeholder="">
      <select v-model="selected" ref="input2">
        <option value='1'>+</option>
        <option value='2'>-</option>
        <option value='3'>*</option>
        <option value='3'>*</option>
        <option value='4'>/</option>
      </select>
      <input ref="input3" v-model="input3"  placeholder="">
      <button v-on:click="cos">result</button>
      <button v-on:click="cos0">清零</button>
      <p ref="input5" v-text="input5"></p>
      <div class="jsqbox">
        <div class="jsq">
          <button value="1" v-on:click="sz(1)">1</button>
          <button value="2" v-on:click="sz(2)">2</button>
          <button value="3" v-on:click="sz(3)">3</button>
          <button value="+" v-on:click="fh('+')">+</button>
          <button value="4" v-on:click="sz(4)">4</button>
          <button value="5" v-on:click="sz(5)">5</button>
          <button value="6" v-on:click="sz(6)">6</button>
           <button value="-" v-on:click="fh('-')">-</button>
          <button value="7" v-on:click="sz(7)">7</button>
          <button value="8" v-on:click="sz(8)">8</button>
          <button value="9" v-on:click="sz(9)">9</button>
          <button value="*" v-on:click="fh('*')">*</button>
          <button value="0" v-on:click="sz(0)">0</button>
          <button v-on:click="sz('00')">00</button>
          <button v-on:click="sz('000')">000</button>           
          
          <button value="/" v-on:click="fh('/')">/</button>
          <button value="" v-on:click="enter">enter</button>
          <button value="" v-on:click="del">del</button>
          <button value="" v-on:click="clear">clear</button>
          <button value="" v-on:click="retn">retn</button>
          <p v-text="process"></p>
          <p v-text="result"></p>
          <!-- <p v-text="result1"></p> -->
          <br/>
          <p v-text="result2"></p>
          <br/>
          <p v-text="result3"></p>
        </div>
      </div>

      <div class="jsqbox1">
        <div class="jsq1">
          <p class="jsqxsq">0</p>
          <button>CE</button>
          <button>C</button>
          <button>←</button>
          <button>÷</button>
          <button>7</button>
          <button>8</button>
          <button>9</button>
          <button>X</button>
          <button>4</button>
          <button>5</button>
          <button>6</button>
          <button>-</button>
          <button>1</button>
          <button>2</button>
          <button>3</button>
          <button>+</button>
          <button>±</button>
          <button>0</button>
          <button>.</button>
          <button>=</button>
        </div>
      </div>
  </div>

</template>
<script>
  export default {
    data:()=> {
        return {
            gg: '',
            gg2: '',
            gg3: '',
            selected: '',
            input1: '',
            input3: '',
            input5: '',
            process:'',
            process1:'',
            result:'',
            result4n:0,
            result4:[],
            result1:'2+3*4-5*6/3-7',
            result2:'',
            result3:'',
        }
    },
    methods: {
      cos:function(e){
        if(this.$refs.input2.value == 1){
          this.input5  = parseInt(this.input1) + parseInt(this.input3)
        }else if(this.$refs.input2.value == 2){
          this.input5 = this.input1 - this.input3
        }else if(this.$refs.input2.value == 3){
          this.input5 = this.input1 * this.input3
        }else if(this.$refs.input2.value == 4){
          this.input5 = this.input1 / this.input3
        }else{
          alert("错误")
        }
      },
      cos0:function(e){
        this.input5 = 0
        this.input1 = ""
        this.input3 = ""
      },
      sz:function(e){
        this.process = this.process + e
      },
      fh:function(e){
        if(this.process.length > 0){
          var regPos = /^\d+(\.\d+)?$/;
          var regNeg = /^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$/;
          if(regPos.test(this.process.charAt(this.process.length - 1)) || regNeg.test(this.process.charAt(this.process.length - 1))) {
            this.process = this.process + e
          } else {
            this.process = this.process.substring(0,this.process.length-1) + e
          }
        }
      },
      enter:function(e){
        // var regPos = /^\d+(\.\d+)?$/;
        // var regNeg = /^(-(([0-9]+\.[0-9]*[1-9][0-9]*)|([0-9]*[1-9][0-9]*\.[0-9]+)|([0-9]*[1-9][0-9]*)))$/;
        // if(regPos.test(this.process.charAt(this.process.length - 1)) || regNeg.test(this.process.charAt(this.process.length - 1))) {
        //     // this.result = eval(this.process)
        //     // this.process = this.result
        //   } else {
        //     // alert("格式错误")
        //   }
        // this.process = "2+5";
        var ss = this.process;
        this.result4n++;
        this.result4[this.result4n] = this.result;
        if(ss.indexOf('+') != -1){
          console.log("+")
           this.result = parseFloat(ss.split("+")[0]) + parseFloat(ss.split("+")[1]);
        }else if(ss.indexOf('-') != -1){
          console.log("-")
          this.result = ss.split("-")[0] - ss.split("-")[1];
        }else if(ss.indexOf('*') != -1){
          console.log("*")
          this.result = ss.split("*")[0] * ss.split("*")[1];
        }else if(ss.indexOf('/') != -1){
          console.log("/")
          this.result = ss.split("/")[0] / ss.split("/")[1];
        }else{
          this.result = this.process
        }
        this.process = "" + this.result
        // console.log(ss)

      },
      del:function(e){
        console.log(this.process.length)
        console.log(this.process)
        this.process = this.process.substring(0,this.process.length-1)
        console.log(this.process)
      },
      clear:function(e){
        this.process = ""
        this.result = ""
      },
      retn:function(e){
        if(this.result4n < 2){
          alert("没有回退了")
        }else{
          this.result = "" + this.result4[this.result4n];
          this.process = "" + this.result4[this.result4n];
          this.result4n--
        }
       
      }
    }
  }
</script>
<style>
:root {
  --mainColor:red;
  --onewidth:100%;
  --oneheight:500px;
  --boxBgColor:#ccc;
  --btnBColor:#fff;
  --btnBRcolor:#ccc;
  --pJbColor1:#fff;
  --pJbcolor2:color(#000 alpha(50%));
  --PColor:#000;
}
body {
  color: var(--mainColor);
  font-family: system-ui;
  overflow-wrap: break-word;
  background:--mainColor;
}
.jsqbox1{
  width:var(--onewidth);
  height:var(--oneheight);
  display: flex;
  justify-content: center;
  align-items:center
}
.jsq1{
  width:240px;
  height:240px;
  background:var(--boxBgColor);
  overflow: hidden;
}
 
.jsq1 button{
  width:60px;
  height:38px;
  line-height:38px;
  text-align:center;
  background-color:var(--btnBColor);
  border:1px solid var(--btnBRcolor);
  font-size:20px;
}
 
.jsq1 p{
  color:var(--PColor);
  width:100%;
  height:40px;
  line-height:40px;
  font-size:22px;
  font-weight:bold;
  text-align:right;
  padding:0;
  margin:0;
  background:linear-gradient(to left,var(--pJbColor1), var(--pJbcolor2));
  margin-bottom:5px;
}

</style>
