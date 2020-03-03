<template>
	<div class="container">
		<b-table striped hover :items="items" :fields="fields" @row-clicked="goPokemon"></b-table>
	</div>
</template>

<script>
export default {
	props: {
		items: {
			type: Array,
			default: []
		}
	},
	data() {
		return {
			fields: [{ key: 'name', label: 'Item', }]
		}
	},
	methods: {
		goPokemon(record, index) {
			this.$router.push({path: `/items/${record.name}`});
		}
	}
}
</script>