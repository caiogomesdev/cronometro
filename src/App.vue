<template>
  <div id="app">
    <img class="img" src="./assets/cronometro.png" />
    <a class="timer">{{zfill(hour)}}:{{zfill(min)}}:{{zfill(sec)}}</a>

    <div class="btns">
      <button class="btn" @click="play">{{isPlaying !== null ? "PAUSAR" :"VAI" }}</button>
      <button class="btn" @click="clear">LIMPAR</button>
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
      isPlaying: null,

    }
  },
  methods: {
    zfill(number){
      return number.toString().padStart(2,0)
    },
    play(){
      
      if(this.isPlaying === null){
        this.playing()
        this.isPlaying = setInterval(()=> this.playing(), 1000)
      }
      else{
        clearInterval(this.isPlaying);
        this.isPlaying = null;
        this.pause();
      }
    },
    playing(){
      this.sec++
      if(this.sec >= 60){
        this.sec = 0;
        this.min++;
      }
      if(this.min >= 60){
        this.min = 0;
        this.hour++;
      }

    },
    pause(){
      console.log("Pause")

    },
    clear(){
      this.sec = 0;
      this.min = 0;
      this.hour = 0;

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
  margin: 0px 7px;
  padding: 6px;
  cursor: pointer;
  transition: all ease-in-out .3s;
}
.btn:hover{
  opacity: 0.8;
}
</style>
