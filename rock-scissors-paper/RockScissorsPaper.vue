<template>
    <div>
        <div id ="computer" :style="{ background: 'url(https://en.pimg.jp/023/182/267/1/23182267.jpg) ${imgCoord} 0'}"></div>
        <div>
            <button @click="onClickButton('바위')">바위</button>
            <button @click="onClickButton('가위')">가위</button>
            <button @click="onClickButton('보')">보</button>
        </div>
        <div>{{result}}</div>
        <div>현재 {{score}}</div>
        </div>
</template>

<script>
const rspCoords = {
        rock: '0',
        scissors: '-142px',
        paper : '-284px'
    };

export default {
    
    data() {
        return {
            imgCoord: rspCoords.rock,
            result: '',
            score: '',
        }
    },
    computed: {
        
    },
    methods: {
        onClickButton (choice){
            
        },
    },
}
</script>

<style scoped>
    #computer {
        width: 142px;
        height: 200px;
        background-position: 0 0;
    }
</style>