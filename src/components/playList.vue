<template>
    <div class="playlist">
        <div class="playlist-top">
            <div class="left">
                <svg class="icon" aria-hidden="true">
                    <use xlink:href="#icon-bofang"></use>
                </svg>
                <div class="text">
                    <div class="title">播放全部</div>
                    <div class="num">(共{{playlist.tracks.length}}首)</div>
                </div>
            </div>
            <div class="btn">
                + 收藏 ({{changeValue(playlist.subscribedCount)}})
            </div>
            
        </div>
        <div class="list">
            <div class="playItem" v-for="(item,i) in playlist.tracks" :key="i">
                <div class="left" @click="setPlayIndex(i)">
                    <div class="index">{{i+1}}</div>
                    <div class="content">
                        <div class="title">{{item.name}}</div>
                        <div class="author">
                            <span class="tag" v-for="(tag,idex) in playlist.tags" :key="idex">{{tag}}</span>
                            <span>{{item.al.name}}</span>
                        </div>
                    </div>
                </div>
                <div class="right">
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-bofang1"></use>
                    </svg>
                    <svg class="icon" aria-hidden="true">
                        <use xlink:href="#icon-gengduo-shuxiang"></use>
                    </svg>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import {mapMutations} from 'vuex'
export default{
    props: ['playlist'],
    methods: {
        changeValue:function(num){
            let res = 0
            if(num>=100000000){
                res = num/100000000
                res=res.toFixed(2) + '亿'
            }else if(num>=10000){
                res = num/10000
                res=res.toFixed(2) + '万'
            }
            return res
        },
        ...mapMutations(['setPlayIndex'])
    },

}
</script>
<style lang="less" scoped>
.playlist{
    background-color: #fff;
    border-top-left-radius:0.3rem ;
    border-top-right-radius:0.3rem ;
    width: 7.5rem;
    padding: 0 0.4rem;
    margin-top: 0.4rem;
    .playlist-top{
        display: flex;
        justify-content: space-between;
        height: 1rem;
        align-items: center;
        .left{
            display: flex;
            align-items: center;
            .icon{
                width: 0.6rem;
                height: 0.6rem;
            }
            .title{
                font-size: 0.34rem;
                font-weight: 900;
            }
            .num{
                font-size: 0.24rem;
                color: #666; 
            }
            .text{
                display: flex;
                align-items: center;
                margin-left: 0.2rem;
            }
        }
        .btn{
            font-size: 0.24rem;
            color: #fff;
            background-color: orangered;
            line-height: 0.6rem;
            padding: 0.1rem;
            border-radius: 0.4rem;
        }
    }
    .list{
        .playItem{
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 1rem;

            .left{
                display: flex;
                align-items: center;
                color: #666;
                .index{
                    width: 0.4rem;
                }
                .content{
                    width: 4.5rem;
                    margin-left: 0.4rem;
                    white-space: nowrap; //规定文本不进行换行
                    overflow: hidden;//溢出隐藏
                }
                .title{
                    font-size: 0.3rem;
                    font-weight: 900;
                    color: #000;
                    //margin-bottom: 0.1rem;
                }
                .tag{
                    font-size: 0.1rem;
                    color: orangered;
                    border: 0.5px solid orangered;
                    border-radius: 0.1rem;

                }
                .author{
                    font-size: 0.3rem;
                    color: #666;
                }
            }
            .right{
                .icon{
                    margin:0 0.2rem
                }
            }
        }
    }
}
</style>