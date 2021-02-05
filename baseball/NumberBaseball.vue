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
    return array;
};

export default {
    data() {
        return {
            answer: getNumbers(),   // ex) [1, 2, 3, 4]
            tries: [],              // 시도 횟수
            value: '',              // 입력값
            result: ''              // 결과
        }
    },
    methods: {
        onSubmitForm(e){
            //정답
            if(this.value === this.answer.join('')){
                this.tries.push ({
                    try: this.value,
                    result: '홈런'
                });
                this.result = '홈런';
                this.value = '';
                this.answer = getNumbers();
                this.tries = [];
                this.$refs.answer.focus();

            }else { //오답
                if(this.tries.length >= 9){
                    this.result = `10번 넘게 틀려서 실패! 답은 ${this.answer.join(',')} 이었습니다.`;
                    alert('게임을 다시 시작합니다.');
                    this.value = '';
                    this.result = '';
                    this.answer = getNumbers();
                    this.tries = [];
                    this.$refs.answer.focus();
                }

                let strike = 0;
                let ball = 0;
                const answerArray = this.value.split('').map(v => parseInt(v));
                
                for(let i=0; i<4; i++){
                    if(answerArray[i] === this.answer[i]){
                        strike++;
                    }else if(this.answer.includes(answerArray[i])){
                        ball++;
                    }
                }

                this.tries.push({
                    try : this.value,
                    result: `${strike} Strike, ${ball} ball`
                });

                this.value = '';
                this.$refs.answer.focus();
            }
        }
    },
}
</script>

<style>

</style>