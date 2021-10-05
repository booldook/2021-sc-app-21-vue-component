<template>
	<div class="app-wrapper">
		<ImgCp :title="title" :src="src" />
		<ul class="thumb-wrap">
			<ThumbCp v-for="v in foods" :key="v.id" :img="v" />
		</ul>
	</div>
</template>

<script>
/* 
1. 부모 컴포넌트가 자식 컴포넌트에게 변수를 전달할 때는 v-bind로 전달한다.
2. 자식 컴포넌트는 부모로 부터 props로 변수를 전달받는다.
*/

import axios from 'axios'
import ImgCp from './components/ImgCp.vue'
import ThumbCp from './components/ThumbCp.vue'

export default {
	name: 'App',
	components: { ImgCp, ThumbCp },
	data() {
		return {
			foods: [],
			title: '',
			src: '',
		}
	},
	async created() {
		const { data } = await axios.get('/json/foods.json')
		this.foods = data
		this.title = this.foods[0].title
		this.src = this.foods[0].src
	}
}
</script>

<style lang="scss">
ul, ol {
	list-style: none;
}
.app-wrapper {
	max-width: 400px;
	margin: 2em auto 1em auto;
	.thumb-wrap {
		border: 1px solid #efefef;
		border-radius: .325em;
		padding: .5em;
		display: flex;
		width: 101%;
	}
}
</style>