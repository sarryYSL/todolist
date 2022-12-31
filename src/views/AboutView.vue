<template>
  <div class="section">
    <div class="card-img"></div>
	<div class="card-gao"></div>
	<div class="card-shadow"></div>
  </div>
</template>
<script>
	export default{}
</script>
<style>
	.section{
		position: relative;
		display: flex;
		justify-content: center;
	}
	.card-img{
		display: block;
		position: absolute;	
		width: 276px;
		height: 456px;
		margin: 0 auto;
		border-radius: 20px;
		border: 1px solid black;
		background: #eee url('../assets/card.jpg');
		background-repeat: no-repeat;
		background-size: cover;
		z-index: 1;
		transform: translate3d(20px,20px,20px)
	
	}
	.card-shadow{
		width: 276px;
		height: 456px;
		margin: 0 auto;
		border-radius: 20px;
		transform: translate(30px,30px);
		background-color: #eee;
		z-index: 0;
		position: absolute;
		left: 92%;
		margin-left: -50%;
	}
</style>
