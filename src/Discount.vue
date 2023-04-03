<template>
    <div class="discount" v-if="showDiscount == true">
        <h4>지금 결제하면 {{percent}}% 할인</h4>
    </div>
</template>

<script>
export default {
    name: 'DisCount',
    data(){
        return{
            percent: 30,
            showDiscount: true,
        }
    },
    mounted(){
        setInterval(()=>{
            this.percent-=1;
            if(this.percent <= 0){
                this.showDiscount = false;
            }
        },1000);
    }
}
</script>

<style>
    
</style>