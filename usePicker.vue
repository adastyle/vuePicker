<template>
    <div>
        <div class="box">
            <span>表情 ：</span>
            <div class="select" ref="currPicker" @click="toPicker">请选择</div>
        </div>
        <scroll-picker v-show="selectShow" :PickerPorps="needData" @currpick="handlePick" @pickIsShow="handleIsShow"></scroll-picker>
    </div>
</template>
<script>
import ScrollPicker from './scrollPicker'
export default{
    name : "usePicker",
    data () {
        return {
            needData:{
                columns : ["哈哈","嘿嘿","嘻嘻","呀呀","喔喔","嗯嗯","哇哇"],
                changeBtnSeat :true,   //是否交换确定取消的位置   默认是  ：左取消  右确定
                leftCancel : {
                    type:"cancel",
                    text:"取消",
                    style:{
                        color:"red"
                    },
                    cancelAfterClick :function () {
                        console.log('点击取消之后要干嘛')
                    }
                },
                rightEnsure : {
                    type : "ensre",
                    text : '好了',
                    style:{
                        color:"red",
                        fontWeight:"blod"
                    },
                    ensureAfterClick : function() {
                        console.log('点击确定之后要干嘛')
                    }
                }
            },
            selectShow :false
        }
    },
    components:{
        ScrollPicker
    },
    methods : {
        handlePick (val) {
            console.log(val+"--插件传过来的")
            this.$refs.currPicker.innerHTML=val
        },
        toPicker (self) {
            this.selectShow=true
        },
        handleIsShow (val) {
            this.selectShow=val
        }
    }
}
</script>
<style lang="stylus" scoped>
    .box
        width:100%
        height .8rem
        line-height:.8rem
        display :flex 
        box-sizing:border-box
        padding:0 .2rem
        margin-top:1rem
        .select
            border:1px solid #f5f6f7
            flex:1
            text-align :right
            background:#f5f6f7
            border-radius 4px
            padding-right:.1rem

</style>
