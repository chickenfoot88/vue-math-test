<template>
	<div class="alert alert-secondary">
		<h3>Are you ready?</h3>
		<button @click="$emit('onStart')" type="button" class="btn btn-success">Start</button>
	</div>
</template>

<script>
  export default {

  }
</script>

<style scoped>

  .alert {
    text-align: center;
  }

  h3, .btn {
    margin: 20px 0;
  }

</style>
