<template>
	<b-container>
		<b-row>
			<b-col>
				<listado :items="items"></listado>
			</b-col>
		</b-row>
		<b-row>
			<b-col cols="auto" class="mr-auto"><b-button class="mt-2" v-if="anterior" @click="getAnterior()">Anterior</b-button></b-col>
			<b-col cols="auto" ><b-button class="mt-2" v-if="siguiente" @click="getSiguiente()">Siguiente</b-button></b-col>
		</b-row>
	</b-container>
</template>

<script>

import axios from 'axios'
import listado from '@/components/items/listado.items'

export default {
	components: {
		listado
	},
	watchQuery: ['page'],
	asyncData ({isDev, route, store, env, params, query, req, res, redirect, error}) {
		let page = query.page > 0 ? query.page : 1;
		let limit = 10;
		let offset = (page - 1) * limit; 

		return axios.get(`https://pokeapi.co/api/v2/item/?offset=${offset}&limit=${limit}`).then((res) => {
			return { items: res.data.results, anterior: res.data.previous || '', siguiente: res.data.next || '', page: page };
		}).catch((e) => {
			error({ statusCode: 404, message: 'Page not found' })
		});
	},
	methods: {
		getAnterior() {
			this.$router.push({ path: '/items', query: { page: --this.page }});
		},
		getSiguiente() {
			this.$router.push({ path: '/items', query: { page: ++this.page }});
		}
	}
};
</script>