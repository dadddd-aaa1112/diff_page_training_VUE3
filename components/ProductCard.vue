<template>
	<div class="product-card">
		<img :src="imgUrl" />
		<div class="product-card__info">
			<h2>{{ title }}</h2>
			<p class="price">{{ price }}</p>
			<p class="count">Доступно для доставки {{ count }} шт</p>
			<button @click="addToBasket">Добавить в корзину</button>
		</div>
	</div>
</template>
<script>
export default {
	props: {
		title: {
			type: String,
			validator(value) {
				return value.length < 50
			},
		},
		price: {
			type: Number,
			required: true,
		},
		imgUrl: {
			type: String,
			default:
				'https://avatars.mds.yandex.net/i?id=6c7530e90d0f654fcf1391a54b765783-5485363-images-thumbs&n=13',
		},
		count: {
			type: Number,
			default: 0,
		},
	},
	methods: {
		addToBasket() {
			this.$emit('addToBasket')
		},
	},
}
</script>

<style>
.product-card {
	border: 1px solid rgb(211, 211, 211);
	padding: 20px 15px;
}
.__info {
	margin-top: 20px;
}
h2,
.price {
	font-weight: 500;
}
.count {
	color: rgb(143, 143, 143);
}
button {
	background-color: rgb(221, 56, 56);
	color: #fff;
	border: none;
	border-radius: 4px;
	padding: 8px 14px;
	display: block;
	cursor: pointer;
	margin-top: 20px;
}
</style>
