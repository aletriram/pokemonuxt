<template>
	<div class="container">
		<div class="row">
			<div class="col-12">
				<listado :pokemons="pokemons"></listado>
			</div>
		</div>
		<div class="row">
			<div class="col-6"><b-button v-if="anterior" @click="getAnterior()">Anterior</b-button></div>
			<div class="col-6"><b-button v-if="siguiente" @click="getSiguiente()">Siguiente</b-button></div>
		</div>
	</div>
</template>

<script>

import axios from 'axios'
import listado from '@/components/pokemons/listado.pokemons'

export default {
	components: {
		listado
	},
	data() {
		return {
			pokemons: [],
		}
	},
	asyncData ({isDev, route, store, env, params, query, req, res, redirect, error}) {
		return axios.get(`https://pokeapi.co/api/v2/pokemon/?limit=10`).then((res) => {
			console.log(res.data.results);
			return { pokemons: res.data.results, anterior: res.data.previous || '', siguiente: res.data.next || '' };
		}).catch((e) => {
			error({ statusCode: 404, message: 'Post not found' })
		})
	},
	methods: {
		getAnterior() {
			return axios.get(this.anterior).then((res) => {
				this.pokemons = res.data.results;
				this.anterior = res.data.previous || '';
				this.siguiente = res.data.next || '' ;
			}).catch((e) => {
				error({ statusCode: 404, message: 'Post not found' })
			});
		},
		getSiguiente() {
			return axios.get(this.siguiente).then((res) => {
				this.pokemons = res.data.results;
				this.anterior = res.data.previous || '';
				this.siguiente = res.data.next || '' ;
			}).catch((e) => {
				error({ statusCode: 404, message: 'Post not found' })
			});
		}
	}
};
</script>
