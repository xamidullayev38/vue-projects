<template>
  <div  class="favs" v-for="(item, index) in favs" :key="index" >
    <span>{{ item.from }}</span>
    <span>{{ item.to }}</span>
  </div>
</template>

<script>
export default {
    props: {
        favs: {
            type: Array,
            required: true
        }
    }
}
</script>

<style scoped>
    .favs{
        width: 200px;
        display: flex;
        justify-content: space-between;
    }
    .favs:hover {
        cursor: pointer;
        transform: scale(1.1);
        transition: .4s;
    }
    span{
        width: 80px;
        text-align: center;
        padding: 4px 0;
        background: #290690;
        color: white;
    }
</style>