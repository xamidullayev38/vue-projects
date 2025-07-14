
<script>
export default {
    props: {
        changeAmount: {
            type: Function,
            required: true
        },
        convert: {
            type: Function,
            required: true
        }
    } 
}
</script>

<template>
    <input @input="changeAmount($event.target.value)" min="0" type="number" placeholder="Enter a number">
    <button @click="convert()">Convert</button>

</template>

<style scoped>
button{
    padding: 15px 20px;
    color: #fff;
    text-transform: uppercase;
    cursor: pointer;
    background: #1a032d;
    border: 0;
    border-radius: 3px;
}
    input{
        text-align: center;
        margin: 0 auto;
        display: block;
        padding: 10px 16px;
        border: none;
        background: #222;
        outline: none;
        scroll-behavior: none;
        color: white;
        font-size: 18px;
    }
    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }
</style>