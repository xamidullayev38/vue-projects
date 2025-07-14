
<script>
export default {
    props: {
        setCrypto: {
            type: Function,
            required: true
        }
    },
    data () {
        return {
            current: '',
        }
    },
    methods: {
        setItem(val) {
            this.setCrypto(val)
            this.current = val
        }
    }
}
</script>

<template>
    <ul>
        <li @click="setItem('BTC')" :class="current == 'BTC' ? 'active' : ''">BTC</li>
        <li @click="setItem('USDT')" :class="current == 'USDT' ? 'active' : ''">USDT</li>
        <li @click="setItem('ETH')" :class="current == 'ETH' ? 'active' : ''">ETH</li>
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