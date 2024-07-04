<template>
    <el-container direction="vertical">
        <GameHeader :score="score" :showResult="showResult" v-on:setResult="updateShowResult" ref="GameHeader" />
        <MainSection v-on:setScore="updateScore" v-on:setResult="updateShowResult" v-on:restart="restartGame" :showResult="showResult" :score="score"  />
    </el-container>
</template>

<script>
import GameHeader from './GameHeader.vue';
import MainSection from './MainSection.vue';

// These are the lists used in the application. You can move them to any component needed.


export default{
    name: 'AppHome',
    components: {GameHeader, MainSection},
    data: function(){
        return {score: 0, showResult: false}
    },
    methods: {
        updateScore: function(){
            this.score++;
        },
        updateShowResult: function(){
            this.showResult = true;
            if(this.showResult){
                this.$refs.GameHeader.stopTimer();
            }
        },
        restartGame: function(){
            this.score = 0;
            this.showResult = false;
            this.$refs.GameHeader.onResetTimer();
        }
    }
}
</script>


