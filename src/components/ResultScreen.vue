<template>
	<div class="">
		<h2>Total Success: {{ totalStats.success }}</h2>
		<h2>Total Error: {{ totalStats.error }}</h2>
		<div v-if="stats.success / this.questMax > 0.5" class="alert alert-success">
			<h4>Вы успешно прошли уровень {{ level + 1 }}</h4>
		</div>
		<div v-else class="alert alert-warning">
			<h4>Вы не прошли увровень {{ level + 1 }}. Попробуйте снова.</h4>
		</div>
		<div class="alert alert-primary">
			<hr>
			<h3>Success: {{ stats.success }}</h3>
			<h3>Error: {{ stats.error }}</h3>
	    <hr>
	    <button class="btn btn-default" @click="$emit('repeat')">Repeat</button>
	    <button class="btn btn-default" @click="$emit('nextLevel')" v-if="isEnd() && stats.success / this.questMax > 0.5"> Next Level</button>
	  </div>
	</div>
</template>

<script>
  export default {
    props: ['stats', 'level', 'levels', 'questMax', 'totalStats'],
    methods: {
      isEnd(){
        return this.level+1 < this.levels.length ? true : false
      }
    }
  }
</script>

<style>

</style>
