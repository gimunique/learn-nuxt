<template>
    <div>
        <p>메인 페이지입니다.</p>
        <div>
            <ul>
                <li v-for="product in products" :key="product.id">
                    <img :src="product.imageUrl" alt="product.name">
                    <p>{{ product.name }}</p>
                    <p>{{ product.price }}</p>
                </li>
            </ul>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    // pages 폴더 아래에 위치하는 컴포넌트에만 제공되는 속성
    // 컴포넌트가 생성되기 이전에 호출: asyncData >>> this 접근 불가
    async asyncData() {
        const response = await axios.get('http://localhost:3000/products')
        console.log(response)
        const products = response.data.map(item => {
            return {
                ...item,
                imageUrl: `${item.imageUrl}?random=${Math.random()}`
            }
        })
        return { products }
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
<style>
    
</style>