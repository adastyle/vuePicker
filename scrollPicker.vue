<template>
    <div>
        <div class="shadow" ref="pickerShow"  @click="closePicker"> 
            <div class="content" @click.stop="">
                <div class="controlBtns">
                    <span class="cancel" :style="btnCancelStyle" v-show="cancelIsShow" @click="closePicker">{{this.userInputCancelTxt}}</span>
                    <span class="ensure" :style="btnEnsureStyle" ref="ensurePick" @click="ensurePicker">{{this.userInputEnsureTxt}}</span>
                </div>
                <div class="pickerBox">
                    <div class="picker">
                        <van-picker :columns="columns" @change="onChange" :default-index="2"/>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default{
    name : "ScrollPicker",
    props:{
        needDatas:Object
    },
    data () {
        return {
            cancelIsShow :false,
            columns :this.needDatas.columns,
            leftCancel:this.needDatas.leftCancel,
            rightEnsure:this.needDatas.rightEnsure,
            userInputCancelTxt : "取消",
            userInputEnsureTxt : "确定",
            btnEnsureStyle:{},
            btnCancelStyle:{}
        }
    },
    mounted () {
        //取消btn的显示与否和基本信息
        if(this.leftCancel){
            this.cancelIsShow=true
            if(this.leftCancel.style)
                this.btnCancelStyle = this.leftCancel.style
            if(this.leftCancel.text)
                this.userInputCancelTxt = this.leftCancel.text
        }
        //确定按钮必先显示与是否修改的信息
        if(this.rightEnsure && this.rightEnsure.style)
            this.btnEnsureStyle=this.rightEnsure.style
        if(this.rightEnsure && this.rightEnsure.text)
            this.userInputEnsureTxt=this.rightEnsure.text
    },

    methods : {
        onChange (picker, value, index) {
             localStorage.setItem("ensurePick",value)
        },
        closePicker (){
            this.toUse()
        },
        ensurePicker(){
           let tempPick=localStorage.getItem("ensurePick")
            this.toUse()
           this.$emit("currpick",tempPick)
        },
        //向需要调用组件的上传显示隐藏
        toUse () {
            this.$emit('pickIsShow',false)
        }
    }
}
</script>
<style lang="stylus" scoped>
    .shadow
        position fixed
        top:0
        left:0
        right:0
        bottom:0 
        z-index: 99
        background:rgba(0,0,0,.5)
        .content
            position:absolute
            top:50%
            left:0
            right:0
            bottom:0
            background:#fff
            display:flex
            flex-direction :column
            .controlBtns
                width:100%
                height:1rem
                line-height: 1rem
                background : #f5f6f7
                box-sizing : border-box
                padding:0 .2rem
                color:blue
                text-align:left
                .ensure 
                    float:right
            .pickerBox
                text-align:center
                overflow :hidden 
                color:.15rem
                width:100%
                flex:1
                backgrond:red
                position:relative
                .picker
                    position:absolute
                    top: 50%
                    left:50%
                    transform:translate(-50%,-50%)
                    width:80%
                    height:80%
                    overflow :hidden

</style>