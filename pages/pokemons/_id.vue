<template>
	<b-container>
		<b-row><nuxt-link to="/pokemons">Volver</nuxt-link></b-row>
		<b-row>
			<b-col cols="auto"><b-img :src="pokemon.sprites.front_default" fluid></b-img></b-col>
			<b-col>
				<b-row>
					<b-col><h2>{{pokemon.name}}</h2></b-col>
					<b-col cols="auto"><h3>#{{pokemon.id}}</h3></b-col>
				</b-row>
			</b-col>
		</b-row>
	</b-container>
</template>

<script>
import axios from 'axios'

export default {
	asyncData ({isDev, route, store, env, params, query, req, res, redirect, error}) {

		return axios.get(`https://pokeapi.co/api/v2/pokemon/${params.id}`).then((res) => {
			console.log(res.data);
			return { pokemon: res.data };
		}).catch((e) => {
			error({ statusCode: 404, message: 'Page not found' })
		})
	},
}
</script>