<template>
	<div class="right-bar">
		<div class="user-panel">
			<ul><span class="go-events" @click = "sge = !sge;"><p>Ваші заходи ({{userChoice.length}})
			 <span class ="eyes" v-if ="sge === true"><img src="@/assets/img/eyeloff.svg" alt=""></span>
			 <span class ="eyes" v-else><img src="@/assets/img/eyelonn.svg" alt=""></span>
			</p></span>
				<li :class="{'sge' : !sge}" v-for="uc of showUC" :id = "uc.id">
					<p>{{uc.title}}</p>
					<button class = "btn-rem-ev" @click = "remEve(userChoice)">✖</button>
				</li>
			</ul>

			<ul><span class="go-events" @click = "smg = !smg;"><p>Ймовірні заходи ({{userMaybeGo.length}})
			 <span class ="eyes" v-if ="smg === true"><img src="@/assets/img/eyeloff.svg" alt=""></span>
			 <span class ="eyes" v-else><img src="@/assets/img/eyelonn.svg" alt=""></span>
			</p></span>
				<li :class="{'smg' : !smg}" v-for="umg of showMaybe" :id = "umg.id">
					<p>{{umg.title}}</p>
					<button class = "btn-rem-ev" @click = "remEve(userMaybeGo)">✖</button>
				</li>
			</ul>

			<ul><span class="go-events" @click = "sse = !sse;"><p>Збереженно ({{userSaved.length}})
			 <span class ="eyes" v-if ="sse === true"><img src="@/assets/img/eyeloff.svg" alt=""></span>
			 <span class ="eyes" v-else><img src="@/assets/img/eyelonn.svg" alt=""></span>
			</p></span>
				<li :class="{'sse' : !sse}" v-for="us of showSaved" :id = "us.id">
					<p>{{us.title}}</p>
					<button class = "btn-rem-ev" @click = "remEve(userSaved)">✖</button>
				</li>
			</ul>
			
		</div>
	</div>
</template>

<script>
export default{
	props:['userChoice','userMaybeGo','userSaved'],	// Take arr from content
	data(){
		return{
			sge:true,	//Show Go Events
			smg:true,	//Show Maybe Go
			sse:true	//Show Save Events
		}
	},
	methods:{
		remEve(arr){
			let crrId = event.target.parentNode.id;
			for (var i=0; i<arr.length;i++){
				if(arr[i].id == crrId){
					return arr.splice(i, 1)
				}
			}		
		}
	},
	computed:{
		showUC(){
			if(this.userChoice.length != 0){
				return this.userChoice
			}else{
				return  
			}
		},
		showMaybe(){
			if(this.userMaybeGo.length != 0){
				return this.userMaybeGo
			}else{
				return  
			}
		},
		showSaved(){
			if(this.userSaved.length != 0){
				return this.userSaved
			}else{
				return  
			}
		}
		
	},
}
</script>

<style>
.eyes{
	position: absolute;
	margin-left: 5%;
	color:white;
	margin-top: -.1rem;

}
.eyes img{
	width: 24px;
	height: 28px;
}

.sge,.smg,.sse{
	display: none;
}
.btn-rem-ev{
	background-color: transparent;
	float:right;
	margin-right: 10px;
	border-radius:.2rem;
	border:none;
	outline: none;
	font-size: 10px;
	color:#3757b8;
	background-color: #d3daf0;
}
.go-events{
	width: 100%;
	height: 30px;
	display: block;
	padding-top:.5rem;	
	margin-top:2%;
	border-top:1px solid #d3daf0;
	border-bottom:1px solid #d3daf0;
	color:#3757b8;
	background-color: #d3daf0;
}
.go-events p {
	text-align: left;
	margin-left: 5%;
}
.go-events:hover{
	
	
}
.right-bar{
	width: 20%;
	height: 95%;
	right: 0px;
	display: inline-block;
	position: absolute;
	background-color: #fff;
	box-shadow: 0 3px 10px rgba(0,0,0,.085);
}
.user-panel ul{
	width: 100%;
	cursor: pointer;
}
.user-panel ul li{
	width: 100%;
	height: 35px;
	text-align: left;
	font-weight: 300;
	font-size: 15px;
	padding-top: 1rem;
	list-style: none;
	background-color: #f0f0f0;
}
.user-panel ul li p{
	display: inline;
	float:left;
	margin-left: 10%;
}
.user-panel ul li:hover{
	background-color:#fcfcfc;
}
</style>