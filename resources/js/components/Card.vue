<template>
	<div class="card relative px-4 py-4 relative card-panel">
    	<h3 class="mb-4" :class="{ 'valid-certificate' : data.is_valid, 'invalid-certificate' : ! data.is_valid }">
    		{{ card.domain }} - {{ data.is_valid ? 'Valid SSL' : 'Invalid SSL' }}
    	</h3>

    	<ul class="list-reset" v-if="! loading && ! error">
      		<li><strong>Issuer: </strong> {{ data.issuer }}</li>
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
