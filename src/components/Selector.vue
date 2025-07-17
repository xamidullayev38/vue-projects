
<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        },
        cryptoNow: {
            type: String,
            required: true
        },
    }
}
</script>

<template>
    <ul>
        <li @click="setCrypto('BTC')" :class="cryptoNow == 'BTC' ? 'active' : ''">BTC</li>
        <li @click="setCrypto('USDT')" :class="cryptoNow == 'USDT' ? 'active' : ''">USDT</li>
        <li @click="setCrypto('ETH')" :class="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
    </ul>
</template>

<style scoped>
    ul{
        list-style-type: none;
        width: 200px;
        padding: 0;
        border-radius: 3px;
        border: 3px solid #000;
    }
    li{
        display: block;
        background: #1A032D;
        color: white;
        padding: 20px 0;
        text-align: center;

    }
    li:hover, li.active{
        background: #24043e;
        cursor: pointer;
    }
</style>