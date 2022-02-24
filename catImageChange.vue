<template>
	<h1>Cat image</h1>
	<img
		src="/kot.jpg"
		:class="classesImg"
		v-if="isVisibleCat"
		:style="changeStyle"
	/>
	<p v-else>open cat...</p>

	<h3>Фильтры</h3>
	<button
		@click="classesImg.sepia = !classesImg.sepia"
		:class="classesImg.sepia ? 'active' : ''"
	>
		Сепия
	</button>
	<button
		@click="classesImg.border = !classesImg.border"
		:class="classesImg.border ? 'active' : ''"
	>
		Рамка
	</button>
	<button
		@click="classesImg.shadow = !classesImg.shadow"
		:class="classesImg.shadow ? 'active' : ''"
	>
		Тень
	</button>

	<button
		@click="isVisibleCat = !isVisibleCat"
		:class="isVisibleCat ? 'active' : ''"
	>
		{{ isCatVisible ? 'display none' : 'show' }}
	</button>

	<h3>Размер</h3>
	<label
		>Ширина {{ currentW }}
		<input
			type="range"
			:value="sizeImg.currentW"
			@input="sizeImg.currentW = $event.target.value"
			:min="sizeImg.minW"
			:max="sizeImg.maxW"
		/>
	</label>

	<label
		>Высота {{ currentH }}
		<input
			type="range"
			:value="sizeImg.currentH"
			@input="sizeImg.currentH = $event.target.value"
			:min="sizeImg.minH"
			:max="sizeImg.maxH"
		/>
	</label>
	<h3>Поворот</h3>
	<label>
		Угол {{ sizeImg.currentRotate }}
		<input
			type="range"
			:value="sizeImg.currentRotate"
			@input="sizeImg.currentRotate = $event.target.value"
			:min="sizeImg.minR"
			:max="sizeImg.maxR"
		/>
	</label>
</template>
<script>
export default {
	data() {
		return {
			classesImg: {
				sepia: false,
				border: false,
				shadow: false,
			},
			isVisibleCat: '',
			sizeImg: {
				currentW: 640,
				currentH: 480,
				minH: 0,
				maxH: 600,
				minW: 0,
				maxW: 800,
				currentRotate: 0,
				minR: 0,
				maxR: 360,
			},
		}
	},
	computed: {
		changeStyle() {
			return {
				width: `${this.sizeImg.currentW}px`,
				height: `${this.sizeImg.currentH}px`,
				transform: `rotate(${this.sizeImg.currentRotate}deg)`,
			}
		},
	},
}
</script>
<style>
.sepia {
	filter: sepia(100%);
}
.border {
	border: 5px dashed purple;
}
.shadow {
	box-shadow: 10px 10px 15px rgba(122, 22, 211, 0.5);
}

.active {
	background-color: red;
}
</style>
