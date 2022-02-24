<template>
	<div class="container">
		<div class="flex">
			<div class="img-wrapper">
				<div>
					<img
						v-if="isCatVisible"
						src="@/assets/2.jpg"
						:class="imgFilters"
						:style="imgStyles"
					/>
					<p v-else>кот скоро вернется</p>
				</div>

				<div class="controls">
					<h1>Шаверма-кот</h1>
					<button
						@click="imgFilters.sepia = !imgFilters.sepia"
						:class="imgFilters.sepia ? 'active' : ''"
					>
						Сепия{{ sepia }}
					</button>

					<button
						@click="imgFilters.border = !imgFilters.border"
						:class="imgFilters.border ? 'active' : ''"
					>
						Рамка
					</button>

					<button
						@click="imgFilters.small = !imgFilters.small"
						:class="imgFilters.small ? 'active' : ''"
					>
						Уменьшить
					</button>

					<h2>Размеры</h2>
					<div class="btn-group">
						<label>
							Ширина: {{ imgSizes.currentWidth }}
							<input
								:value="imgSizes.currentWidth"
								@input="imgSizes.currentWidth = $event.target.value"
								type="range"
								:min="imgSizes.minWidth"
								:max="imgSizes.maxWidth"
							/>
						</label>
						<label>
							Высота: {{ imgSizes.currentHeight }}
							<input
								:value="imgSizes.currentHeight"
								@input="imgSizes.currentHeight = $event.target.value"
								type="range"
								:min="imgSizes.minHeight"
								:max="imgSizes.maxHeight"
							/>
						</label>
					</div>
					<button
						@click="isCatVisible = !isCatVisible"
						:class="imgFilters.small ? 'active' : ''"
					>
						Show
					</button>
				</div>
			</div>
		</div>
	</div>
</template>
<script>
export default {
	data() {
		return {
			isCatVisible: true,
			imgFilters: {
				sepia: false,
				border: false,
				small: false,
			},
			imgSizes: {
				maxWidth: 680,
				maxHeight: 480,
				currentWidth: 680,
				currentHeight: 480,
				minHeight: '',
				minWidth: '',
			},
		}
	},
	computed: {
		imgStyles() {
			return {
				width: `${this.imgSizes.currentWidth}px`,
				height: `${this.imgSizes.currentHeight}px`,
			}
		},
	},
}
</script>
<style>
.container {
	margin-top: 40px;
}
.controls {
	margin-left: 20px;
}

.img-wrapper {
	width: 640px;
	height: 480px;
	background-color: #cecece;
}

.active {
	background-color: teal;
	margin-right: 10px;
}
.sepia {
	filter: sepia(100%);
}
.border {
	border: 5px dashed #464646;
}
.small {
	width: 400px;
}

h2 {
	margin-bottom: 10px;
}
.btn-group {
	margin-bottom: 20px;
}
input[type='range'] {
	display: block;
}
</style>
