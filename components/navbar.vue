<template>
	<div>
		<b-navbar toggleable="lg" type="dark" variant="info">
			<b-navbar-brand to="/">Pokemon nuxt</b-navbar-brand>

			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<b-navbar-nav>
					<b-nav-item to="/pokemons">Pokemons</b-nav-item>
					<b-nav-item to="/items">Items</b-nav-item>
				</b-navbar-nav>

				<!-- Right aligned nav items -->
				<b-navbar-nav class="ml-auto">
					<!-- <b-nav-form>
						<b-form-input size="sm" class="mr-sm-2" placeholder="Buscar..."></b-form-input>
						<b-button size="sm" class="my-2 my-sm-0" type="submit"><i class="fa fa-search"></i></b-button>
					</b-nav-form> -->

					<b-nav-item-dropdown right>
						<!-- Using 'button-content' slot -->
						<template v-slot:button-content>
							<em>User</em>
						</template>
						<b-dropdown-item href="#">Esto es fake</b-dropdown-item>
						<b-dropdown-item href="#">Profile</b-dropdown-item>
						<b-dropdown-item href="#">Sign Out</b-dropdown-item>
					</b-nav-item-dropdown>
				</b-navbar-nav>
			</b-collapse>
		</b-navbar>
	</div>
</template>

<script>
export default {};
</script>