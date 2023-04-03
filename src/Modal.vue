<template>
    <div class="black-bg" v-if="modalIsOpen">
        <div class="white-bg">
        <!-- title, content -->
        <h4>{{oneroom[clIdx].title}}</h4>
        <p>{{oneroom[clIdx].content}}</p>
        <input v-model="month">
        <p>{{month}}개월 선택 시 {{oneroom[clIdx].price * month}}원</p>
        </div>
        <button class="close" @click="$emit('closeModal');">
            X
        </button>
    </div>
</template>

<script>
export default {
    name: 'ModalUi',
    data(){
        return{
            month:1,
        }
    },
    updated(){
        console.log("업데이트.");
        if(this.month == 2){
            alert("수량 2개입니다.");
        }
    },
    watch: {
        month(a){
            //사용자가 month를 글자로 입력하면 경고문 띄우기.
            if(a >= 13){
                alert("13이상 입력하지 마세요.");
                this.month = 1;

            }
            else if(isNaN(a)){
                alert("숫자만 입력하세요.");
                this.month=1;
            }
        }
    },
    props: {
        oneroom : Array,
        clIdx: Number,
        modalIsOpen: Boolean
    }

}
</script>

<style>

</style>