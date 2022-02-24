<template>
	<div class="product-list">
		<div class="flex top-information">
			<h1>Письменные столы</h1>
			<MyInput v-model="searchText" />
			{{ searchText }}

			<button>Найти</button>
		</div>
		<ul class="list-default flex">
			<li v-for="(product, index) in products" :key="index">
				<product-card
					:title="product.title"
					:price="product.price"
					:imgUrl="product.imgUrl"
					:count="product.count"
					@addToBasket="addToBasket(index)"
				/>
			</li>
		</ul>
	</div>
</template>

<script>
import ProductCard from '@/components/ProductCard'
import MyInput from '@/components/MyInput'
export default {
	components: { ProductCard, MyInput },

	data() {
		return {
			searchText: '',
			products: [
				{
					title: 'Стол Jim',
					price: 19999,
					imgUrl:
						'https://avatars.mds.yandex.net/i?id=81728a0e1de1eb4343d9afb91be2b055-4885011-images-thumbs&n=13',
					count: 30,
				},
				{
					title: 'Стол Monako',
					price: 17199,
					imgUrl:
						'https://avatars.mds.yandex.net/i?id=bf29bcdf06a8e610ec8e87d1c6210326-5655860-images-thumbs&n=13',
					count: 20,
				},
				{
					title: 'Стол с двумя ящиками Кварт MD 768',
					price: 10999,
					imgUrl:
						'https://avatars.mds.yandex.net/i?id=9c44743caf536650db4e5cb86ee0c48b-5008692-images-thumbs&n=13',
					count: 23,
				},
			],
		}
	},
	methods: {
		addToBasket(index) {
			console.log(index)
		},
	},
}
</script>

<style>
li {
	margin-right: 20px;
}
.top-information {
	align-items: center;

	margin-bottom: 22px;
}
h1 {
	margin-bottom: 0;
}
button {
	background-color: rgb(221, 56, 56);
	color: #fff;
	border: none;
	border-radius: 4px;
	padding: 8px 14px;
	display: block;
	cursor: pointer;
	margin-left: 10px;
}
</style>
