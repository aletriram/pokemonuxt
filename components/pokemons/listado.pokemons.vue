<template>
	<div>
		<b-table striped hover :items="pokemons", :fields="fields"></b-table>
	</div>
</template>

<script>
export default {
	props: ['pokemons'],
	data() {
		return {
			fields: [{ key: 'name', label: 'Nombre', }]
		}
	}
}
</script>