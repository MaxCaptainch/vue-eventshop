<template>
  <div class="home">
  	<div :class = "{'showModalLog':!showModalLog}" class="background-user-model">
  		
  	</div>
	<div class="nav-bar">
		<div class="logo">
			<img src="@/assets/logo2.png" alt="">
		</div>
		<div class="search">
			<img src="@/assets/loupe.png" alt="">
			<input type="text" id = "search-input" placeholder="Пошук за назвою.." v-model = "search">
		</div>
		<div class="menu">
		<ul>
			
		</ul>
		
		</div>
		<div class="log">
			<button id = "login-btn" @click = "showModalLog = !showModalLog"></button>
		</div>
	</div>
	
  	<div :class = "{'showModalLog':!showModalLog}" class="user-modal"  >
  		<div class="static-modal">
  			<img class = "logo-modal" src="@/assets/logo1.png" alt="">
  			<button class="close-btn-user-modal"  @click = "showModalLog = !showModalLog">✖</button>
  		</div>
  			
  		<div :class = "{'hideLogForm':hideLogForm}" class="log-modal" >
		   	<h3>Вхід</h3>
		   	<input type="email" id = "email"  placeholder="Електронна пошта">
		   	<input type="password"  id = "password" placeholder="Пароль" minlength="8" maxlength="15" >
		   	<button id = "log-btn">Увійти</button>
		   	<button id = "valid-btn" @click = "showRegForm = !showRegForm;hideLogForm = !hideLogForm; ">Зареєструватись</button>
  		</div>
  		
  		<div :class = "{'showRegForm':showRegForm}" class="reg-modal">
  			<h3>Реєстрація</h3>
  			<input type="text" id = "name" placeholder="Ім'я" maxlength="15">
  			<input type="text" id = "Lastname" placeholder="Прізвище">
		   	<input type="email" id = "email" placeholder="Електронна пошта" >
		   	<input type="password" id = "password" placeholder="Пароль" minlength="8" maxlength="15">
		   	<button id = "register-btn">Зареєструватись</button>
		   	<button id = "valid-btn" @click = "hideLogForm = !hideLogForm; showRegForm = !showRegForm">Увійти</button>
		   
  		</div>
  		
   </div>
   <Content :search = "search"/>
  
  </div>
</template>

<script>
import Content from '@/components/content.vue'

export default {
  name: 'Home',
  components: {
    Content
  },
  data(){
  	return{
  		showModalLog:false,
  		hideLogForm:false,
  		showRegForm:false,
  		search:'',
  	}
  },

}


</script>

<style>
/*DYNAMIC CLASS*/
.showModalLog{
	display: none;
}
.hideLogForm{
	opacity: 0 !important;
}
.showRegForm{
	left: 0px !important;
	opacity: 1 !important; 
}
/**/



.home{
	width: 100%;
	height: 100%;
	display: block;
	background-color:#f0f0f0;
	user-select: none;
	font-family: 'Lora', serif;
}

.nav-bar{
	width: 100%;
	height: 5%;
	box-shadow: 0 3px 10px rgba(0,0,0,.085);
	vertical-align: top;
	background-color: #fff;
	border-bottom:1px solid #222629;
}


.logo{
	width: 10%;
	height: 100%;
	left:0px;
	display: inline-block;
	background-color: #fff;
	overflow: hidden;
	border-right:1px solid #222629;
}
.logo img{
	width: 100%;	

	margin: 0;
	padding: 0;
}


.log{
	width: 4%;
	height: 100%;
	background-color: #fff;
	display: inline-block;
	right: 0px;
	vertical-align: top;
	text-align: center;
	border-left:1px solid #222629;
}
#login-btn{
	margin: 0;
	padding: 0;
	width: 35px;
	height: 35px;
	margin-left: 1rem;
	border:none;
	background-color: transparent;
	background-image: url('../assets/user.svg');
	outline: none;
}
.user-modal{
	width: 300px;
	height: 350px;
	position: absolute;
	background-color: #fff;
	z-index: 3;
	margin: 0 auto;
	padding: .5rem;
	left: 0px;
	right: 0px;
	top:90px;
	text-align: center;
	border-radius: .5rem;
	box-shadow: 0 3px 10px rgba(0,0,0,.085);
	z-index: 6;
	
}
.static-modal{
	height: 20%;
}
.close-btn-user-modal{
	position: absolute; 
	margin: 0 auto;
	right: 5px;
	background-color: transparent;
	border:none;
	outline:none;
	font-size: 20px;
}
.log-modal, .reg-modal{
	width: 100%;
	height: 80%;
	transition: 1s;
	left: 0px;
	position: absolute;

}
.background-user-model{
	width: 100%;
	height: 100%;
	position: absolute;
	background-color: #000;
	z-index: 1;
	opacity: 0.9;

}
.reg-modal{
	
	opacity:0;
}

.search{
	width: 30%;
	height: 100%;
	display: inline-flex;
	overflow: hidden;
	vertical-align: top;
	position: relative;
	
}
.search img{
	width: 24px;
	height: 24px;
	margin: 5px ;
	vertical-align: top;
	display: inline-flex;
}	
#search-input{
	width: 90%;
	height: 100%;
	font-size: 18px;
	padding-left: .5rem;

	border:none;
	outline: none;
	
	
}

.menu{
	width: 55%;
	height: 100%;
	vertical-align: top;
	display: inline-block;
	position: relative;
	display: inline-flex;
}

.menu ul{
	width: 100%;
	height: 100%;
	position: relative;
	margin: 0px;
	padding: 0px;
	display: inline-flex;
	overflow: hidden;
}
.menu ul li{
	width: 15%;
	height: 90%;
	border-right:1px solid #222629;
	display: inline;
	background-color: #222629;
	color: #fff;
	text-transform: uppercase;
	text-align: center;
	padding-top: 0.4rem;
	margin-left: 1rem;
}
.user-modal input{
	height: 25px;
	display: block;
	margin: 0 auto;
	margin-top: 1rem;
	left: 0px;right: 0px;
	
	width: 60%;
	border:none;
	border-bottom:1px solid #222629;
	outline: none;
	background-color: transparent;
}


.user-modal .log-modal button, .user-modal .reg-modal button{
	margin: 0 auto;
	margin-top: 1rem;
	display: block;
	left: 0px;
	right: 0px;
	padding: .3rem 1.5rem;
	border: 0.09rem solid #e3e3e3;
	border-radius: .2rem;
	 
	color: #fff;
	text-decoration: none;
	background-color: #222629;
	outline: none;
}
#valid-btn{
	background-color: transparent;
	border:none;
	margin: 0 auto;
	position: absolute;
	bottom:20px ;
	color:#222629;
}



</style>