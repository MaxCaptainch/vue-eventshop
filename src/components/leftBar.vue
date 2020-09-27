<template>
	<div class = "left-bar">
		<div class="filters">
			<select class = "sort" v-model="sortBy" @click = "$emit('change-sort', sortBy);">
			    <option :value="null">Тип сортування:</option>
			    <option value="by-views-f-more">По переглядам ⬆️</option>
			    <option value="by-views-f-less">По переглядам ⬇️ </option>
			    <option value="by-date-f-new">Незабаром 📅 </option>
			    <option value="by-date-f-old">Пізніше 📅 </option>
 			 </select>
			<ul><span @click = "showCities = !showCities;" class = "filters-component"><p>Місто</p></span>	
				<li :class="{'showCities' : !showCities}" v-for="city of Cities" >
					<input type="checkbox" class = "custom-checkbox" :id = "city.title" name = "city" :value = "city.title" @click = "filtersItems();">
					<label :for="city.title">{{city.title}}</label>
				</li>
			</ul>
			<ul><span  @click = "showCategories = !showCategories" class = "filters-component"><p>Категорія</p></span>
				<li :class="{'showCategories' : !showCategories}" v-for="category of Categories" >
					<input type = "checkbox" class = "custom-checkbox" :id = "category.title" name = "category" :value = "category.title" @click = "filtersItems();">
					<label :for="category.title" >{{category.title}}</label>
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default{
	
	data(){
		return{
			Cities:[
				{
					title: 'Київ'
				},
				{
					title: 'Харків'
				},
				{
					title: 'Одесса'
				},
				{
					title: 'Львів'
				},
				{
					title: 'Днепр'
				},
				{
					title: 'Запоріжжя'
				},
				{
					title: 'Ужгород'
				},
			],

			Categories:[
				{
					title: 'IT'
				},
				{
					title: 'Кіно'
				},
				{
					title: 'Танці'
				},
				{
					title: 'Розваги'
				},
				{
					title: 'Для дітей'
				},
			],
			
			showCities:false,
			showCategories:false,
			sortBy: null,
			elemFilter:null,
		}

	},
	methods:{
		filtersItems(){
			
			this.elemFilter = event.target.value;
			this.elemFilterName = event.target.name;
			this.$emit('filters-items', this.elemFilter, this.elemFilterName);
			
			
		}
	},
	
	
}
</script>

<style>
.showCities, .showCategories{
	display: none;
}
.left-bar{
	width: 15%;
	height: 95%;
	display: inline-block;
	left:0px;
	box-shadow: 0 3px 10px rgba(0,0,0,.085);
	overflow-y: scroll;
	overflow-x: hidden;
}
.filters{
	width: 100%;
	height: 100%;
	top:0px;
	background-color: #fff;
	overflow-x: hidden;
	overflow-y: scroll;
	text-align: center;
	font-size: 17px;
}


.filters ul, .favorites ul{
	width: 100%;
	cursor: pointer;
}
.filters ul li, .favorites ul li{
	width: 100%;
	height: 35px;
	text-align: left;
	font-weight: 300;
	padding-left: 2%;
	font-size: 15px;
	padding-top: 0.5rem;
}

.filters ul li:hover, .favorites ul li:hover{
	background-color: #f0f0f0;
	
}

.filters-component{
	width: 100%;
	height: 30px;
	display: block;
	text-align: left;
	padding-top:.5rem;	
	margin-top:2%;
}
.filters-component p{
	margin-left: 3%;
}

.filters-component:hover{
	color:#3757b8;
	background-color: #d3daf0;
}

select, option{
	width: 95%;
	height: 5%;
	font-size:17px;	
	text-align: center;	
	margin: 5% 0% 5%;
	outline: none;
	font-family: 'Lora', serif;
}

/*CHECKBOXS*/
.custom-checkbox {
  position: absolute;
  z-index: -1;
  opacity: 0;
}
.custom-checkbox+label {
  display: inline-flex;
  align-items: center;
  user-select: none;
}
.custom-checkbox+label::before {
  content: '';
  display: inline-block;
  width: 1em;
  height: 1em;
  flex-shrink: 0;
  flex-grow: 0;
  border: 1px solid #3757b8;
  border-radius: 0.25em;
  margin-right: 0.5em;
  background-repeat: no-repeat;
  background-position: center center;
  background-size: 50% 50%;
}
.custom-checkbox:checked+label::before {
  border-color: #3757b8;
  background-color: #3757b8;
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 8 8'%3e%3cpath fill='%23fff' d='M6.564.75l-3.59 3.612-1.538-1.55L0 4.26 2.974 7.25 8 2.193z'/%3e%3c/svg%3e");
}
.custom-checkbox:not(:disabled):not(:checked)+label:hover::before {
  border-color: #3757b8;
}
/* стили для активного состояния чекбокса (при нажатии на него) */
.custom-checkbox:not(:disabled):active+label::before {
  background-color: #3757b8;
 
}

</style>