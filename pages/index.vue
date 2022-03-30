<template>
<div class="app">
	<main>
	<div>
		<input type="text">
	</div>
	<ul>
		<li class="item flex" 
			v-for="product in products" 
			:key="product.id" 
			@click="moveToDetailPage(product.id)"
		>
		<img class="product-image" :src="product.imageUrl" :alt="product.name">
		<p>{{ product.name }}</p>
		<span>{{ product.price }}</span>
		</li>
	</ul>
	</main>
	<!-- <ProductList></ProductList> -->
</div>
</template>
<script>
import axios from 'axios';
// import ProductList from '~/components/ProductList.vue'

export default {
	// components: { ProductList }
	// [pages 폴더 아래에 위치하는 컴포넌트에만] 제공되는 속성
	// 컴포넌트가 생성되기 이전에 호출: asyncData >>> this 접근 불가
	// asyncData는 뷰 컴포넌트에서 제공하는 인스턴스 옵션 속성
	async asyncData() {
	const response = await axios.get('http://localhost:3000/products')
	// console.log(response)
	const products = response.data.map(item => {
			return {
				...item,
				imageUrl: `${item.imageUrl}?random=${Math.random()}`
			}
		})
		return { products }
	},
	methods: {
		moveToDetailPage(id) {
			console.log(id)
			// nuxt는 라우터를 내부적으로 품고 있음
			this.$router.push(`detail/${id}`)
		}
	},
	/* data() {
		return {
			products: [],
		}
	},
	async created() {
		const response = await axios.get('http://localhost:3000/products')
		console.log(response)
		this.products = response.data;
	}, */
}

</script>
<style scoped>
.flex {
	display: flex;
	justify-content: center;
}

.item {
	display: inline-block;
	width: 400px;
	height: 300px;
	text-align: center;
	margin: 0 0.5rem;
	cursor: pointer;
}

.product-image {
	width: 400px;
	height: 250px;
}

.app {
	position: relative;
}

.cart-wrapper {
	position: sticky;
	float: right;
	bottom: 50px;
	right: 50px;
}

.cart-wrapper .btn {
	display: inline-block;
	height: 40px;
	font-size: 1rem;
	font-weight: 500;
}

</style>  