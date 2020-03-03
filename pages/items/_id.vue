<template>
	<b-container>
		<b-row>
			<b-col>
				<b-button :to="this.enlaceBack" class="mt-2">Volver</b-button>
			</b-col>
		</b-row>
		<b-row>
			<b-col cols="auto"><b-img :src="item.sprites.default" fluid></b-img></b-col>
			<b-col>
				<b-row>
					<b-col><h2>{{item.name}}</h2></b-col>
					<b-col>Precio: {{item.cost}}<img src="@/assets/images/pokemondollar_1.png"></b-col>
					<b-col cols="auto"><h3>#{{item.id}}</h3></b-col>
				</b-row>
				<div class="row">
					<b-col>
						<h4>Efectos</h4>
						<b-list-group>
							<b-list-group-item v-for="(effect, index) in item.effect_entries" :key="index">{{effect.short_effect}}</b-list-group-item>
						</b-list-group>
					</b-col>
				</div>
			</b-col>
		</b-row>
		<b-row>
			
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

		return axios.get(`https://pokeapi.co/api/v2/item/${params.id}`).then((res) => {
			return { item: res.data };
		}).catch((e) => {
			error({ statusCode: 404, message: 'Page not found' })
		})
	},
	computed: {
		enlaceBack() {
			if (this.item && this.item.id) {
				let page = Math.floor(this.item.id / 10) + 1
				return `/items?page=${page}`;
			} else return '/items'
		}
	}
}
</script>