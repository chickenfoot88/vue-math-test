<template>
  <div class="alert alert-primary">
    <h3>Success: {{ stats.success }}</h3>
    <h3>Error: {{ stats.error }}</h3>
    <hr>
    <button class="btn btn-default" @click="$emit('repeat')">Repeat</button>
    <button class="btn btn-default" @click="$emit('nextLevel')" v-if="isEnd()"> Next Level</button>
  </div>
</template>

<script>
  export default {
    props: ['stats', 'level', 'levels'],
    methods: {
      isEnd(){
        return this.level+1 < this.levels.length ? true : false
      }
    }
  }
</script>

<style>

</style>
