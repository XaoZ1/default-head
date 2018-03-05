<template>
    <img class="img" v-if="logo != '' && logo != null" :src="logo" />
    <div class="img-bg" v-else ref="img_bg">
        <span ref="icon" class="iconfont icon-circle"></span>
        <!-- <div class="inset-bg" ref="inset_bg"> -->
        <div ref="name" class="img-name">{{formatValue}}</div>

    </div>
</template>

<script>
export default {
    props: ['userName', 'size', 'logo'],
    data () {
        return {
            formatValue: ''
        }
    },
    created () {
    },
    watch: {
        userName () {
            console.log(this.userName)
            console.log(this.logo)
            this.customStyle()
            this.formatFunction()
        }
    },
    mounted () {
        setTimeout(() => {
            this.customStyle()
            this.formatFunction()
        }, 500)
    },
    methods: {
        formatFunction () { // 格式化名字
        // console.log(this.userName)
            let temValue = ''
            let secondValue = ''
            if (this.userName) {
                temValue = this.userName.substring(0, 1)
                secondValue = this.userName.substring(1, 2)
            }
            // let temValue = this.userName.substring(0, 1)
            // console.log(temValue)
            // console.log(secondValue)
            // console.log(/^[a-zA-Z]$/.test(temValue))
            // console.log(/^[\u4E00-\u9FA5]$/.test(temValue))
            if (/^[a-zA-Z]$/.test(temValue)) {
                // this.formatValue = 
                if (/^[a-zA-Z]$/.test(secondValue)) {
                    this.formatValue = temValue.toUpperCase() + secondValue.toLowerCase()
                } else if (/^[\u4E00-\u9FA5]$/.test(secondValue)) {
                    this.formatValue = temValue
                }
            } else if (/^[\u4E00-\u9FA5]$/.test(temValue)) {
                this.formatValue = temValue
            }
        },
        customStyle () { // 自定义样式
            if (this.$refs.name) {
                this.$refs.img_bg.style.width = this.size + 'px'
                this.$refs.img_bg.style.height = this.size + 'px'
                // this.$refs.img_bg.style.padding = (this.size * 4) / 70 + 'px'

                this.$refs.icon.style.fontSize = this.size + 'px'
                this.$refs.icon.style.lineHeight = this.size + 'px'
                
                // this.$refs.inset_bg.style.width = this.size - ((this.size * 4) / 70 * 2) + 'px'
                // this.$refs.inset_bg.style.height = this.size - ((this.size * 4) / 70 * 2) + 'px'
                // this.$refs.inset_bg.style.marginLeft =  - (this.size / 2) + 'px'
                // this.$refs.inset_bg.style.marginTop =  - (this.size / 2) + 'px'

                this.$refs.name.style.lineHeight = this.size + 'px'
                this.$refs.name.style.fontSize = parseInt((this.size * 38) / 70) + 'px'
            }
            
        }
    }
}
</script>

<style lang="scss" scoped>
.img-bg {
    // background:#fff;
    // padding: 4px;
    // border-radius: 50%;
    display: inline-block;
    position: relative;
    .icon-circle {
        // width: 100%;
        // height: 100%;
        color:#ffb54a;
        position: absolute;
        top: 0;
        left: 0;
    }
    .img-name {
        font-weight: bold;
        color:#ffb54a;
        text-align: center;
    }
}
</style>
