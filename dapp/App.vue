<script>
import { mapGetters } from 'vuex';
import MetaMask from './components/MetaMask';
export default {
    components: {
        MetaMask,
    },
    computed: {
        ...mapGetters([
            'routerState'
        ])
    },
    methods:{
        onComplete(msg){
            console.log('msg:', msg);
        }
    }
}
</script>

<template>
    <div id="app">
        <meta-mask
            userMessage="null"
            @onComplete="onComplete">
        </meta-mask>

        <img id="logo" src="~logo.png" alt="">
        <div class="menu_box">
            <router-link v-for="(item, i) in routerState" :to='item.url' :key='i'>
                {{ item.link }}
            </router-link>
        </div>
        
        <transition mode='out-in'>
            <router-view></router-view>
        </transition>
    </div>
</template>

<style lang='scss' scoped>
    .v-enter-active, .v-leave-active{
        transition: opacity .2s;
    }
    .v-enter, .v-leave-active{
        opacity:0;
    }
    #app{
        width: 100%;
        height: 100%;
        padding-top: 50px;
        img#logo{
            width: 100px;
            margin: 0 auto;
        }
        .menu_box{
            width: 30%;
            margin: 0 auto;
            overflow: hidden;
            margin-top: 30px;
            >a{
                display: block;
                width: 33.333%;
                float: left;
                text-align: center;
                font-size: 22px;
                color: #999;
            }
        }
    }
</style>