<template>
    <div class="playController">
        <div class="left" @click="show=!show">
            <img :src="playlist[playCurrentIndex].al.picUrl" alt="">
            <div class="content">
                <div class="title">{{playlist[playCurrentIndex].name}}</div>
                <div class="tips">横划可以切换上下首哦</div>
            </div>
        </div>
        <div class="right">
            <svg v-if="paused" class="icon" aria-hidden="true" @click="play">
                <use xlink:href="#icon-icon--"></use>
            </svg>
            <svg v-else class="icon" aria-hidden="true" @click="play">
                <use xlink:href="#icon-zanting"></use>
            </svg>
            <svg class="icon" aria-hidden="true">
                <use xlink:href="#icon-liebiao"></use>
            </svg>
        </div>
        <play-music :play="play" :paused="paused" @back="show=!show" v-show="show" :playDetail="playlist[playCurrentIndex]"></play-music>
        <audio ref="audio" :src="`https://music.163.com/song/media/outer/url?id=${playlist[playCurrentIndex].id}.mp3`"></audio>
    </div>
</template>

<script>
import {mapState,mapMutations} from 'vuex'
import  playMusic from '@/components/playMusic.vue';
 export default{
    data(){
        return{
            paused:true,
            show:false
        }
    },
    computed: {
        ...mapState(['playlist','playCurrentIndex'])
    },
    mounted () {
        console.log(this.$refs.audio);
        this.$store.dispatch('reqLyric',{id:this.playlist[this.playCurrentIndex].id})
        this.UpdateTime()
    },
    updated () {
        console.log(this.playlist[this.playCurrentIndex]);
        this.$store.dispatch('reqLyric',{id:this.playlist[this.playCurrentIndex].id})
    },
    methods: {
        play:function(){
            if(this.$refs.audio.paused){
                this.$refs.audio.play()
                this.paused = false;
                this.UpdateTime()
            }else{
                this.$refs.audio.pause()
                this.paused = true;
                clearInterval(this.$store.state.id)
            }
            console.log([this.$refs.audio]);
            
        },
        UpdateTime(){
            this.$store.state.id = setInterval(()=>{
                this.$store.commit('setCurentTime',this.$refs.audio.currentTime)
            },1000)
        }
    },
    components: {
        playMusic
    }


}
</script>


<style lang="less" scoped>

.playController{
    background:#fff;
    width: 7.5rem;
    height: 1.2rem;
    position: fixed;
    left: 0;
    bottom: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-top: 1px solid #ccc;
    .left{
        display: flex;
        padding: 0 0.2rem;
        img{
            width: 0.8rem;
            height: 0.8rem;
            border-radius: 0.4rem;
        }
        .content{
            width: 4.5rem;
            padding:0 0.2rem;

            .title{
                white-space: nowrap; //规定文本不进行换行
                overflow: hidden;//溢出隐藏
            }
            .tips{
                font-size: 0.2rem;
                color: #999;
            }
        }
    }
    .right{
        .icon{
            width: 0.4rem;
            height: 0.4rem;
            margin: 0 0.2rem;
        }
    }
}
</style>