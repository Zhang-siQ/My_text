<template>
    <div>
        <div class="write"></div>
        
        <van-tabbar v-model="active">
            
            <van-tabbar-item icon="home" @click="gotoHome()">
                首页
            </van-tabbar-item>
            <van-tabbar-item icon="shop" @click="gotoNews()">产品管理</van-tabbar-item>
            <van-tabbar-item icon="logistics" @click="gotoControl()">销售管理</van-tabbar-item>
            <van-tabbar-item icon="chat" @click="gotoMeg()">消息</van-tabbar-item>
            <van-tabbar-item icon="contact" @click="gotoMe()">我的</van-tabbar-item>
        </van-tabbar>
        <router-view></router-view>
        <div class="write1"></div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            active: 0
        }
    },
    created () {
        this.websochetInit ()
    },
    methods: {
        gotoHome() {
            this.$router.push('./HomePage')
        },
        gotoNews() {
            this.$router.push('./ProductControl')
        },
        gotoControl() {
            this.$router.push('./Market')
        },
        gotoMeg() {
            this.$router.push('./Messages')
        },
        gotoMe() {
            this.$router.push('./myCompany')
        },
        websochetInit () {
        this.websock = new WebSocket('ws://218.89.39.165:5030/hn/webSocket2');
        this.websock.onmessage = function (val) {
            cordova.plugins.notification.local.schedule({
            id: 1,
            title: '7857',
            icon: 'https://ss0.bdstatic.com/94oJfD_bAAcT8t7mm9GUKT-xh_/timg?image&quality=100&size=b4000_4000&sec=1530258815&di=adb6a61a476f5c826eeb3b490b930f74&src=http://09.imgmini.eastday.com/mobile/20160509/20160509160024_3d5fd2648fa5f2cf5aec916b736a53f3_2.jpeg',
            text: val.data,
            foreground: true,
            actions: [
                { id: 'yes', title: '确认查看' },
                { id: 'no',  title: '忽略' }
            ]
        })
            cordova.plugins.notification.local.on('yes', function (notification,eopts) {
            alert(JSON.stringify(notification))
            })
            cordova.plugins.notification.local.on('no', function (notification,eopts) {
            alert(JSON.stringify(eopts))
            })
            cordova.plugins.notification.local.on('clear', function(notification){
            alert('clear')
            })
            cordova.plugins.notification.local.on('cancel', function(notification){
            alert('cancel')
            })
            cordova.plugins.notification.local.on('click', function(notification, eopts,state){
            alert('click')
            })
        };

        }
    }
}
</script>

<style lang="scss">

    
    
</style>
