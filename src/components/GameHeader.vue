<template>
    <el-header class="header-bg">
        <el-row type="flex" justify="space-between" class="row-bg">
            <el-col :span="4">
                <div class="logo-container">
                    <img src="https://assets.ccbp.in/frontend/react-js/match-game-website-logo.png" alt="website-logo" />
                </div>
            </el-col>
            <el-col :span="6">
                <div class="info-bg">
                    <p>score: <span>{{score}}</span></p>
                    <p>
                        <img src="https://assets.ccbp.in/frontend/react-js/match-game-timer-img.png" alt="timer" class="timer-img" />
                        <span>{{time}} sec</span>
                    </p>
                </div>
            </el-col>
        </el-row>
    </el-header>
</template>

<script>
export default{
    name: 'GameHeader',
    props: {score: Number, showResult: Boolean},
    data(){
        return {time: 60, timerId: ''}
    },
    methods: {
        setTimer: function(){
            this.timerId = setInterval(()=>{
                if(this.time <= 0){
                    clearInterval(this.timerId);
                    this.$emit('setResult');
                }else{
                    this.time--;
                }
            }, 1000);
        },
        onResetTimer: function(){
            clearInterval(this.timerId);
            this.time = 60;
            this.setTimer();
        },
        stopTimer: function(){
            clearInterval(this.timerId);            
        }
    },
    mounted(){
        this.setTimer();
    }
}
</script>

<style scoped>

.header-bg{    
    height: 80px;
    background-color: #2c0e3a;
    display: flex;
    align-items: stretch;
}

.row-bg{
    flex-grow: 1;
}

.logo-container{
    height: 100%;
    padding: 10px;
    display: flex;
    align-items: center;
}

.logo-container img{
    height: 40px;
}

.info-bg{
    height: 100%;
    padding: 10px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

.info-bg p{
    color: #ffffff;
    font-size: 18px;
    font-weight: 500;
    margin: 0px 0px 0px 22px;
    display: flex;
    align-items: center;
}

.info-bg span{
    color: #fec653;
    font-weight: 550;
    font-size: 24px;
}

.timer-img{
    width: 24px;
    height: 24px;
    margin-right: 5px;
}

</style>