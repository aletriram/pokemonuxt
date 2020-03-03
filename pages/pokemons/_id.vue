<template>
	<b-container>
		<b-row>
			<b-col>
				<b-button :to="this.enlaceBack" class="mt-2">Volver</b-button>
			</b-col>
		</b-row>
		<b-row>
			<b-col cols="auto"><b-img :src="pokemon.sprites.front_default" fluid></b-img></b-col>
			<b-col>
				<b-row>
					<b-col><h2>{{pokemon.name}}</h2></b-col>
					<b-col cols="auto"><h3>#{{pokemon.id}}</h3></b-col>
				</b-row>
			</b-col>
		</b-row>
		<b-row>
			<b-col>
				<b-button :to="this.enlaceBack" class="mt-2 mb-2">Volver</b-button>
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
	computed: {
		enlaceBack() {
			if (this.pokemon && this.pokemon.id) {
				let page = Math.floor(this.pokemon.id / 10) + 1
				return `/pokemons?page=${page}`;
			} else return '/pokemons'
		}
	}
}
</script>