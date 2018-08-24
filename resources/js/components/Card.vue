<template>
	<div class="card relative px-4 py-4 relative card-panel">
		<div>
    		<h3 class="mb-4">{{ card.domain }}</h3>
    	</div>

    	<ul class="list-reset" v-if="! loading && ! error">
      		<li><strong>Issuer: </strong> {{ data.issuer }}</li>
      		<li><strong>Valid: </strong> {{ data.is_valid ? 'Yes' : 'No' }}</li>
      		<li><strong>Expiration: </strong> {{ data.expiration_date }}</li>
    	</ul>

    	<div v-else>
    		{{ error }}
    	</div>
	</div>
</template>

<script>
export default {
    props: ['card'],

    data() {
    	return {
    		data: [],
    		loading: false,
    		error: null,
    	}
    },

    mounted() {
    	this.loading = true;

        Nova.request()
        	.get(`/nova-vendor/nova-ssl-card/details`, {
        		params: {
            		domain: this.card.domain
           		}
        	})
        	.then(response => {
        		this.data = response.data;
        		this.loading = false;
        	})
        	.catch(({response}) => {
        		this.error = response.data.error;
        		this.loading = false;
        	})
    },
}
</script>
