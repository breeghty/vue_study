<template>
    <div v-for="(room,i) in oneroom" :key="room">
        <img :src="oneroom[i].image" class='room-img' alt="방 이미지">
        <h4 @click="$emit('openModal', oneroom[i].id);">{{oneroom[i].title}}</h4>
        <p>{{oneroom[i].content}}</p>
        <p>{{oneroom[i].price}}원</p>
    </div>
</template>

<script>
export default {
    name: 'CardUi',
    props:{
        oneroom: Array,
        
    }
}
</script>

<style>

</style>