<template>
	<section>  
    <div class="container">
      <div class="row">
        <div v-for="(list,index) in habis" :key="index" class="col-md-6">
          <div class="progress-wrap">
            <h3>{{list.nombre}}</h3>
            <div class="progress">
              <div class="progress-bar" role="progressbar" aria-valuenow="90"
                  aria-valuemin="0" aria-valuemax="100" 
                  :style="{'width': list.porcentaje +'%'}">
                  <span>{{list.porcentaje}}%</span>
              </div>
            </div>
          </div>
        </div>          
      </div>
    </div>
  </section>
</template>

<script>
	export default {
		data() {
			return {
				habis: []
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
			}
		}
		
	}
	
</script>
