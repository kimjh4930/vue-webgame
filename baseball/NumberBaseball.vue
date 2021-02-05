<template>
  <div>
      <h1>{{result}}</h1>
      <form @submit.prevent="onSubmitForm">
        <input ref="answer" minlength="4" maxlength="4" v-model="value">
        <button>입력</button>
      </form>
      <div>시도 : {{tries.length}}</div>
      <div>{{answer}}</div>
      <ul>
        <li v-for="t in tries" v-bind:key="t.try">
            <div>{{t.try}}</div>
            <div>{{t.result}}</div>
        </li>
      </ul>
  </div>
</template>

<script>
const getNumbers = () =>{
    const candidates = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    const array = [];

    for(let i=0; i < 4; i++){
        const chosen = candidates.splice(Math.floor(Math.random() * (9-i)), 1)[0];
        array.push(chosen);
    }

    console.log("array : " + array);

    return array;
};

const check = (answer, value) => {
    const board = [false, false, false, false];
    var strike = 0;
    var ball = 0;

    for(var i=0 ; i<4; i++){
        if(parseInt(value[i]) === parseInt(answer[i])){
            strike++;
            board[i] = true;
        }
    }

    for(var i=0; i<4; i++){
        console.log(answer.includes(value[i]));
        if(answer.includes(parseInt(value[i])) && board[i] === false){
            ball++;
        }
    }

    const result = strike + ' Strike, ' + ball + ' Ball';
    console.log(result);

    return result;
}

export default {
    data() {
        return {
            answer: getNumbers(),
            value: '',
            result: '',
            tries: []
        }
    },
    methods: {
        onSubmitForm(e){
            console.log(this.value);

            this.tries.push({
                try : this.value,
                result: check(this.answer, this.value)
            });

            if(this.tries.length >= 10){
                this.tries = [];
                this.answer = getNumbers();
            }
            
            this.$refs.answer.focus();
            this.value = '';
        }
    },
}
</script>

<style>

</style>