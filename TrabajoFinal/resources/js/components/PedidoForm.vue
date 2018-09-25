<template>
	<div>
		<div class="alert alert-success" v-if="saved">
			<strong>Success!</strong> Your pedido has been saved successfully.
		</div>

		<div class="well well-sm" id="pedido-form">
			<form class="form-horizontal" method="post" @submit.prevent="onSubmit">
				<div class="form-group">
					<label>persona_id</label>
					<input type="text" v-model="pedido.persona_id" class="form-control input-sm" placeholder="Id de la persona del pedido">
				</div>
				<div class="form-group">
					<label>Vianda_id</label>
					<input type="text" v-model="pedido.vianda_id" class="form-control input-sm" placeholder="Id de la vianda del pedido">
				</div>
				<div class="form-group">
					<label>Fecha de solicitud</label>
					<input type="text" v-model="pedido.fecha_solicitud" class="form-control input-sm" placeholder="Fecha de solicitud del pedido">
				</div>
				<div class="form-group">
					<label>Fecha de entrega</label>
					<input type="text" v-model="pedido.fecha_entrega" class="form-control input-sm" placeholder="Fecha de entrega del pedido">
				</div>
				<button type="submit" class="btn btn-primary">Guardar</button>
			</form>
		</div>
	</div>
</template>

<script>
export default {

	data() {
		return {
			errors: [],
			saved: false,
			pedido: {
				persona_id: null,
				vianda_id: null,
				fecha_solicitud: null,
				fecha_entrega: null
			}
		};
	},

	methods: {
		onSubmit() {
			this.saved = false;

			axios.post('api/pedidos', this.pedido)
			.then(({data}) => this.setSuccessMessage())
			.catch(({response}) => this.setErrors(response));
		},

		setErrors(response) {
			this.errors = response.data.errors;
		},

		setSuccessMessage() {
			this.reset();
			this.saved = true;
		},

		reset() {
			this.errors = [];
			this.pedido = {persona_id: null, vianda_id: null, fecha_solicitud: null, fecha_entrega: null};
		}
	}
}
</script>