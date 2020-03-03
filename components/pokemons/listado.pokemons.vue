<template>
	<div class="container">
		<b-table striped hover :items="pokemons" :fields="fields" @row-clicked="goPokemon"></b-table>
	</div>
</template>

<script>
export default {
	props: {
		pokemons: {
			type: Array,
			default: []
		}
	},
	data() {
		return {
			fields: [{ key: 'name', label: 'Nombre', }]
		}
	},
	methods: {
		goPokemon(record, index) {
			console.log(record);
			this.$router.push({path: `/pokemons/${record.name}`});
		}
	}
}
</script>