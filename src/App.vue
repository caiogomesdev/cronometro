<template>
  <div id="app">
    <img class="img" src="./assets/cronometro.png" />
    <a class="timer">{{zfill(hour)}}:{{zfill(min)}}:{{zfill(sec)}}</a>

    <div class="btns">
      <button class="btn btn-margin" @click="play">{{timer !== null ? "PAUSAR" :"VAI" }}</button>
      <button class="btn btn-margin" @click="clear">LIMPAR</button>
    </div>

    <div class="interval" v-show="intervalList.length > 0">
      <ul>
        <li v-for="interval in intervalList" :key="interval" >VOCÊ PAUSOU EM {{interval}}</li>
      </ul>
      <button class="btn" @click="clearIntervalList">LIMPAR HISTÓRICO</button>
    </div>

  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      sec: 0,
      min: 0,
      hour: 0,
      timer: null,
      intervalList: []
    }
  },
  methods: {
    zfill(number){
      return number.toString().padStart(2,0)
    },
    play(){
      
      if(this.timer === null){
        this.playing()
        this.timer = setInterval(()=> this.playing(), 1000)
      }
      else{
        clearInterval(this.timer);
        this.timer = null;
        this.pause();
      }
    },
    playing(){
      this.sec++
      if(this.sec >= 59){
        this.sec = 0;
        this.min++;
      }
      if(this.min >= 59){
        this.min = 0;
        this.hour++;
      }

    },
    pause(){
      this.intervalList.push(`${this.zfill(this.hour)}:${this.zfill(this.min)}:${this.zfill(this.sec)}`)
      console.log(this.intervalList)
    },
    clear(){
      if(this.timer !== null){
        clearInterval(this.timer)
        this.timer = null
      }
      this.sec = 0;
      this.min = 0;
      this.hour = 0;
      this.clearIntervalList();
    },
    clearIntervalList(){
      this.intervalList = []
      console.log(this.intervalList)
    }

  }

}
</script>

<style>
#app{
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.img{
  width: 420px;
  height: 420px;
  padding-top: 100px;

}
.timer{
  color: #fff;
  font-size: 70px;
  margin-top: -210px;
}
.btns{
  margin-top: 155px;
  display: flex;
}
.btn{
  -webkit-user-select: none;
  -moz-user-select: none;

  width: 150px;
  background-color: #fff;
  font-size: 20px;
  border: none;
  border-radius: 5px;
  text-align: center;
  padding: 6px;
  cursor: pointer;
  transition: all ease-in-out .3s;
}
.btn-margin{
  margin: 0px 7px;
}
.btn:hover{
  opacity: 0.8;
}
.interval{
  color: #fff;
  flex: 1;
  width: 420px;
  margin-top: 15px;
}
.interval ul{
  text-align: center;
}
.interval ul li{
  list-style: none;
  background-color: rgb(70,70,70);
  padding: 15px;
  margin-bottom: 10px;
}

</style>
