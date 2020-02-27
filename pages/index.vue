<template>
	<div class="container">
		<listado :pokemons="pokemons"></listado>
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
		return axios.get(`https://pokeapi.co/api/v2/pokemon/`).then((res) => {
			return { pokemons: res.data.results };
		}).catch((e) => {
			error({ statusCode: 404, message: 'Post not found' })
		})
	}
};
</script>
