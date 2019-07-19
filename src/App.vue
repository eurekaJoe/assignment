<template>
  <div class="box1" id="app">

    <ul class="items list-inline" >
      <li class="cheats"> <u class="cl"></u> <u class="cr"></u> <i></i><strong>是否开启作弊</strong>
        <p>{{list.cheats?'YES':'NO'}}<br /></p>
      </li>
      <li class="game_mode"> <u class="cl"></u> <u class="cr"></u> <i></i><strong>游戏模式</strong>
        <p v-if="list.game_mode=='SANDBOX'">SANDBOX<br />沙盒模式</p>
        <p v-if="list.game_mode=='CAREER'">CAREER<br />职业模式</p>
      </li>
      <li class="max_players"> <u class="cl"></u> <u class="cr"></u> <i></i><strong>服务器玩家上限</strong>
        <p>{{list.max_players}} 人<br /></p>
      </li>
      <li class="mod_control"> <u class="cl"></u> <u class="cr"></u> <i></i><strong>是否开启mod控制</strong>
        <p v-if="!list.mod_control">否</p>
        <p v-if="list.mod_control">是</p>
      </li>
      <!--<li class="player_count"> <u class="cl"></u> <u class="cr"></u> <i></i><strong>在线玩家数</strong>
        <p>{{list.player_count}} 人<br /></p>
      </li>-->
    </ul>

    <div class="grid" >
        <div class="box">
          <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
            <line class="top" x1="0" y1="0" x2="900" y2="0"/>
            <line class="left" x1="0" y1="460" x2="0" y2="-920"/>
            <line class="bottom" x1="200" y1="260" x2="-600" y2="260"/>
            <line class="right" x1="200" y1="0" x2="200" y2="1380"/>
          </svg>
          <h3>A</h3>
          <span>联机端口</span>
          <span>{{list.port}}</span>
        </div>
        <div class="box">
          <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
            <line class="top" x1="0" y1="0" x2="900" y2="0"/>
            <line class="left" x1="0" y1="460" x2="0" y2="-920"/>
            <line class="bottom" x1="200" y1="260" x2="-600" y2="260"/>
            <line class="right" x1="200" y1="0" x2="200" y2="1380"/>
          </svg>
          <h3>A</h3>
          <span>服务器名称</span>
          <span>{{list.server_name}}</span>
        </div>
        <div class="box">
          <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
            <line class="top" x1="0" y1="0" x2="900" y2="0"/>
            <line class="left" x1="0" y1="460" x2="0" y2="-920"/>
            <line class="bottom" x1="200" y1="260" x2="-600" y2="260"/>
            <line class="right" x1="200" y1="0" x2="200" y2="1380"/>
          </svg>
          <h3>S</h3>
          <span>宇宙大小</span>
          <span>{{list.universeSize}}</span>
        </div>
        <div class="box">
          <svg xmlns="http://www.w3.org/2000/svg" width="100%" height="100%">
            <line class="top" x1="0" y1="0" x2="900" y2="0"/>
            <line class="left" x1="0" y1="260" x2="0" y2="-920"/>
            <line class="bottom" x1="200" y1="260" x2="-600" y2="260"/>
            <line class="right" x1="200" y1="0" x2="200" y2="1380"/>
          </svg>
          <h3>S</h3>
          <span>插件版本</span>
          <span>{{list.version}}</span>
        </div>
    </div>

  </div>
</template>

<script src="vue.min.js"></script>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data(){
    return{
      list:[]
    };
  },
  methods: {
    getData:function() {
      var instance=axios.create();
      instance.defaults.timeout=2500;
      instance.get('http://ksp.debug.online:6703/',{
        timeout:5000,
        headers: { "Access-Control-Allow-Origin": "*" }
      })
      .then(response => {
          this.list=response.data;
          console.log(response.data);
      })
      .catch(response =>{
        console.log('error');
      })
    },

  },
  mounted() {
    this.getData();
  }
}
</script>

//document.getElementById("cheats").innerHTML="cheats:"+JSON.stringify(response.data);
<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
}
</style>
