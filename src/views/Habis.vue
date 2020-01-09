<template>
	<div class="container">
		<h1>Habilidades</h1>

		<form @submit.prevent="agregar()">
			<h3>agregar nueva habilidad</h3>
			<input type="text" class="form-control my-2" placeholder="Nombre" v-model="habi.nombre">
			<input type="text" class="form-control my-2" placeholder="Porcentaje" v-model="habi.porcentaje">
			<b-button class="btn-success my-2 btn-block" type="submit">Agregar</b-button>
		</form>

		<table class="table">
		<thead>
			<tr>
				<th scope="col">#</th>
				<th scope="col">Nombre</th>
				<th scope="col">Porcentaje</th>
				<th scope="col">Acciones</th>			
			</tr>
		</thead>
		<tbody>
			<tr v-for="(item,index) in habis" :key="index">
				<th scope="row">{{index+1}}</th>
				<td>{{item.nombre}}</td>
				<td>{{item.porcentaje}}</td>
				<td>
					<b-button>Accion</b-button>
					<!-- <b-button @click="eliminarNota(item._id)" 
					class="btn-danger btn-sm mx-2">Eliminar</b-button>

					<b-button @click="activarEdicion(item._id)" 
					class="btn-warning btn-sm">Editar</b-button> -->
				
				</td>
			</tr>
		</tbody>
	</table>

	</div>
</template>

<script>
	export default {
		data() {
			return {
				habis: [],
				habi: {nombre: '', porcentaje: ''}
			}
		},
		created(){
			this.listar();
		},
		methods: {
			listar(){
				this.axios.get('/habi')
				.then(res => {
					console.log(res.data);
					this.habis = res.data;
				})
				.catch(e => {
					console.log(e.response);
				})
			},
			agregar(){
				// console.log(this.habi);
				this.axios.post('/nueva-habi', this.habi)
				.then(res => {
					this.habis.push(res.data)
					this.habi.nombre = '';
					this.habi.porcentaje = '';
				})
				.catch(e => {
					console.log(e.response);
				})
			}
		}
		
	}
	

</script>