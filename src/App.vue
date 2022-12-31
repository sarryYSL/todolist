<template>
  <div id="app">
	<div class="index" :style="{'background-image':'url('+bgUrl+')'}">
		<nav>
			<div class="btn-bg" @click="changeBg()">点击更换背景</div>
		</nav>
    <router-view/>
	</div>
  </div>
</template>
<script>
	export default{
		data(){
			return{
				bgUrl: require('./assets/bg/banner9.png'),
			}
		},
		methods:{
			changeBg(){
				// 取随机数0-9
				let imgs=[
					require('./assets/bg/banner1.png'),
					require('./assets/bg/banner5.jpg'),
					require('./assets/bg/banner6.jpeg'),
					require('./assets/bg/banner8.jpg'),
					require('./assets/bg/banner9.png'),
					require('./assets/bg/banner10.jpg')];
					this.bgUrl = imgs[Math.floor(Math.random() *6)] ;
			}
		}
	}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.btn-bg{
	
	cursor: pointer;
}
.index{
	width: 100%;
	height: 100vh;
	background-size: cover;
	background-repeat: no-repeat;
}
nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>


