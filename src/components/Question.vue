<template>
  <div class="alert">
    <h3>{{ x }} + {{ y }} = ?</h3>
    <hr>
    <div class="buttons">
      <button class="btn btn-success"
              v-for="number in answers"
              @click="onAnswer(number)"
      >
        {{ number }}
      </button>
    </div>
  </div>
</template>

<script>
  export default {
		// Принимаем данные от родителя App
    props: ['settings'],
    data(){
      return {
				// Генерация слагаемых
        x: mtRand(this.settings.from, this.settings.to),
        y: mtRand(this.settings.from, this.settings.to)
      }
    },
    computed: {
			//Верный ответ
      good(){
        return this.x + this.y
      },
			//Неверные ответы
      answers(){
        let res = [this.good];

        while(res.length < this.settings.variants){
          let num = mtRand(this.good - this.settings.range, this.good + this.settings.range)
					// Проверка повторных ответов
          if(res.indexOf(num) === -1){
            res.push(num)
          }
        };
				// Сортировка массива с ответами
        return res.sort(function(){
          return Math.random() > 0.5;
        });
      }
    },
    methods: {
			//Проверка правильности ответа
      onAnswer(num){
        if(num == this.good){
					// Верный ответ вызывает событие success, которое пробрасывается в родителя
          this.$emit('success')
        } else {
					// Неверный ответ вызывает событие error, которое пробрасывается в родителя
          this.$emit('error', `${this.x} + ${this.y} = ${this.good}!`)
        }
      }
    }
  }

	// Рандомизаторм слагаемых
  function mtRand(min, max){
    let diff = max - min;
    return Math.floor(Math.random() * (diff + 1)) + min
  }
</script>

<style scoped>
  .alert {
    padding: 30px;
    background-color: #eee;
  }

  .buttons {
    display: flex;
    justify-content: space-around;
  }

  .btn {
    margin: 20x 0;
  }
</style>
