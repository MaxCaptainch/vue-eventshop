<template>
<div class = "main">
	<div class="event-added-window" :class="{'sEventAdded' : sEventAdded}">
			<span>Подія вже додана до вашого списку </span>
			<p>✔️</p>
	</div>
	<leftBar v-on:change-sort = "changeSort"
			 v-on:filters-items = "filtersImets"
	/>
	<div class="content">
		
		<div class="event"   :id ="event.id" v-for="event of sortedItems">
			<div class="event-info" >
				<section class="event-info-main">
					<h2>{{event.title}}</h2>
					<p><img src="@/assets/img/date.svg" class = "icons"> {{event.time | formatDate}}</p>
					<p><img src="@/assets/img/map.svg" class = "icons">  {{event.location}}</p>
					<p><img src="@/assets/img/link.svg" class = "icons"> {{event.site}}</p>
				</section>
				<section class="event-info-vitag"><span class = "event-info-views"><img src="@/assets/img/eye.svg" class = "icons"> {{event.views}} </span> <p v-for="tag of event.tags" class = "tags"> {{tag}}</p></section>
				<section class="event-info-description">
					<p>{{event.description}}</p>
				</section>
			</div>
			<div class="event-buttons">
				<button @click = "addEvent();">Піду</button>
				<button @click = "addMaybe();">Можливо</button>
				<button @click = "addSaved();">Зберегти</button>
			</div>	
		</div>
	
	</div>
	<rightBar :userChoice = "userChoice" :userMaybeGo = "userMaybeGo" :userSaved = "userSaved"/>
</div>
</template>
<script>
import leftBar from '@/components/leftBar.vue'
import rightBar from '@/components/rightBar.vue'
import eventsJson from '../events.json'
export default{
	components:{
		leftBar,
		rightBar
	},
	props:['search'],
	data(){
		return{
			events: eventsJson,
			sortBy:null,
			filteredByChoice:[],
			filterName:null,
			userChoice:[],
			userMaybeGo:[],
			userSaved:[],
			sEventAdded:false,
		}
	},
	methods:{
		changeSort(sortBy){
			this.sortBy = sortBy;
		},
		filtersImets(elemFilter, elemFilterName){
			this.filterName = elemFilterName;
			if(this.filteredByChoice.indexOf(elemFilter) != -1){
				this.filteredByChoice = this.filteredByChoice.filter(function(item){
					return item !== elemFilter
				})
			}
			else{
				this.filteredByChoice.push(elemFilter);
				
			}
		},

		sortItem(){

			if(this.sortBy === null){
				return this.events
			};
			if(this.sortBy === 'by-views-f-more'){
				return this.events.sort((prev, curr) => {
					return curr.views - prev.views;
			});};

			if(this.sortBy === 'by-views-f-less'){
				return this.events.sort((prev, curr) => {
					return prev.views - curr.views;
			});};
				
			if(this.sortBy === 'by-date-f-new'){
				return this.events.sort((prev, curr) => {
					return prev.time - curr.time; 
			});};
		
			if(this.sortBy === 'by-date-f-old'){
				return this.events.sort((prev, curr) => {
					return curr.time - prev.time;
			});};

		},
		searchFunc(){
				if(this.search != ''){
					let obj = this.events;
					let newArray = [];
					let search = this.search;
					
					for (let key in obj){
						let el = obj[key];
						if (el.title.toUpperCase().includes(search.toUpperCase()))newArray.push(el);
					}
					return newArray;
			}
		},
		addEvent(){
			let crrId = event.target.parentNode.parentNode.id;
			let events = this.events;
			let uc = this.userChoice;
			function isPositive(el){
				return el.id != crrId
			}	
			for(let i = 0; i<events.length;i++){
				if(events[i].id == crrId){
					if(uc.length == 0){
						uc.push(events[i]);
					}
					else if(uc.every(isPositive) === true){
						uc.push(events[i]);
					}
					else{
						let shw=()=>{this.sEventAdded = !this.sEventAdded;}
						shw();
						setTimeout(shw, 2500);
					}
					
				}
			}
		},
		addMaybe(){
			let crrId = event.target.parentNode.parentNode.id;
			let events = this.events;
			let umg = this.userMaybeGo;
			function isPositive(el){
				return el.id != crrId
			}	
			for(let i = 0; i<events.length;i++){
				if(events[i].id == crrId){
					if(umg.length == 0){
						umg.push(events[i]);
					}
					else if(umg.every(isPositive) === true){
						umg.push(events[i]);
					}
					else{
						let shw=()=>{this.sEventAdded = !this.sEventAdded;}
						shw();
						setTimeout(shw, 2500);
					}
					
				}
			}
		},
		addSaved(){
			let crrId = event.target.parentNode.parentNode.id;
			let events = this.events;
			let us = this.userSaved;
			function isPositive(el){
				return el.id != crrId
			}	
			for(let i = 0; i<events.length;i++){
				if(events[i].id == crrId){
					if(us.length == 0){
						us.push(events[i]);
					}
					else if(us.every(isPositive) === true){
						us.push(events[i]);
					}
					else{
						let shw=()=>{this.sEventAdded = !this.sEventAdded;}
						shw();
						setTimeout(shw, 2500);
					}
					
				}
			}
		},


		

		
	},
	computed:{
		sortedItems(){
			if(this.search != ''){
				return this.searchFunc();
			}
			this.sortItem();
			if (this.filterName == 'city'){
				if(this.filteredByChoice.length !== 0){
				return this.events.filter((elem)=>{
					return this.filteredByChoice.includes(elem.location);
				})
				}else{
					return this.events
				}
			}
			if(this.filterName == 'category'){
				if(this.filteredByChoice.length !== 0){
					return this.events.filter((elem)=>{
						return this.filteredByChoice.includes(elem.tags[0]) || this.filteredByChoice.includes(elem.tags[1])
					})			
				}else{
					return this.events
				}
			}
		
			return this.events
		
		},
	
	},
	filters:{
			formatDate(time){
				return Intl.DateTimeFormat('ru').format(time);
			},
	},
	
}
</script>
<style>

.event-added-window{
	width: 250px;
	height: 75px;
	position: absolute;
	margin: 0 auto;
	left: 0;right: 0;
	top:15%;
	opacity: 0;
	z-index: 5;
	background-color: #96ffad;
	border-radius: .2rem;
	text-align: center;
	padding: 2rem;
	font-size: 18px;
	transition: 1s;
}
.sEventAdded{
	opacity: 1;
}
	.main{
		width: 100%;
		height: 100%;
		overflow: hidden;
	}
	.content{
		width:65%;
		height: 95%;
		
		display: inline-block;
		position: absolute;
		overflow-y: scroll;
	}

	.event{
		width: 55%;
		height: 50%;
		margin: 0 auto;
		margin-top:3%;
		margin-bottom: 3%;
		background-color: #fff;
		box-shadow: 0 3px 10px rgba(0,0,0,.085);
		padding: 1% 3% 2% 3%;
	}
	.event-info {
		width: 100%;
		height: 90%;
		
	}
	
	.event-info-main{
		width: 75%;
		height: 40%;
		float:left;
		font-size: 15px;
		
	}

	.event-info-vitag{
		margin-top:0.5rem;
		width: 20%;
		float:right;
	}
	.event-info-views{
		width: 100%;
		text-align: right;
		float: right;
		margin-bottom: 5px;
	}
	.tags{
		display: inline-block;
		margin: .2rem;
		background-color: #222629;
		padding: .2em .8em .2em;
		border-radius: .3rem;
		color:#fff;
		font-size: 14px;
	}
	.event-info-main h2{
		text-align: center;
		margin-bottom: 0.8rem;
		font-weight: 500;
		font-size: 24px;
	}
	.event-info-main a{
		color:black;
		text-decoration: none;
	}
	
	.icons{
		width: 14px;
		height: 14px;
		
	}
	.event-conditions p{
		display: inline-block;
	}
	.event-info-description{
		width: 100%;
		height: 50%;
		right:0px;
		display: inline-block;
		overflow: hidden;
		margin-top: .3em;
		text-align: justify;
		font-size: 14px;
		
	}
	.event-buttons{
		width: 100%;
		height: 10%;
		text-align: center;
		bottom:0px;
		margin: 0;
	}
	.event-buttons button{
		display: inline-block;
		margin-left: 0.5rem;
	    padding: .3rem 1.5rem;
	    margin-right: 0.10rem;
	    border: 0.09rem solid #222629;
	    border-radius: .2rem;
	    background-color: #222629;
	    color: #fff;
	    text-decoration: none;

		outline: none;
	}

	.event-buttons button:hover{
		background-color: transparent;
   		
   		color:#222629;
	}


*::-webkit-scrollbar
{
    width: 0;
}

/* ie 10+ */
*
{
    -ms-overflow-style: none;
}

/* фф (свойство больше не работает, других способов тоже нет)*/
*{
    overflow: -moz-scrollbars-none;
}

.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
</style>