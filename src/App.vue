<script>

    import Input from './components/Input.vue';
    import Selector from './components/Selector.vue';
    import CryptoConvert from 'crypto-convert';

    const convert = new CryptoConvert();
    export default{
        components: { Input, Selector },
        data () {
            return{
                amount: 0,
                cryptoFirst: '',
                cryptoSecond: '',
                error: '',
                result: 0
            }
        },
        methods: {
            changeAmount(val) {
                this.amount = val
            },
            setCryptoFirst(val) {
                this.cryptoFirst = val
            },
            setCryptoSecond(val) {
                this.cryptoSecond = val
            },
            async convert() {
                if(this.amount <= 0){
                    this.error = 'Enter number upper than zero'
                    return 
                }else if (this.cryptoFirst == '' || this.cryptoSecond == ''){
                    this.error = 'Chose currency'
                    return
                } else if (this.cryptoFirst == this.cryptoSecond){
                    this.error = 'Enter different currency'
                    return
                }
                this.error = ''

                await convert.ready(); 
	
                if(this.cryptoFirst == 'BTC' && this.cryptoSecond =="ETH"){
                    this.result = convert.BTC.ETH(this.amount);
                }else if(this.cryptoFirst == 'BTC' && this.cryptoSecond =="USDT"){
                    this.result = convert.BTC.USDT(this.amount);
                }else if(this.cryptoFirst == 'USDT' && this.cryptoSecond =="BTC"){
                    this.result = convert.USDT.BTC(this.amount);
                }else if(this.cryptoFirst == 'USDT' && this.cryptoSecond =="ETH"){
                    this.result = convert.USDT.ETH(this.amount);
                }else if(this.cryptoFirst == 'ETH' && this.cryptoSecond =="BTC"){
                    this.result = convert.ETH.BTC(this.amount);
                }else if(this.cryptoFirst == 'ETH' && this.cryptoSecond =="USDT"){
                    this.result = convert.ETH.USDT(this.amount);
                }
            }
        }
    }
</script>

<template>
    <div class="wrapper">
        <h1>CRYPTO</h1>
        <Input :changeAmount="changeAmount" :convert="convert"/>
        <p v-if="error != ''">{{ error }}</p>
        <p v-else-if="result !== 0" class="result-text">{{ result }} </p>
        <div class="selectors">
            <Selector :setCrypto="setCryptoFirst"/>
            <Selector :setCrypto="setCryptoSecond"/>
        </div>
    </div>    
</template>

<style scoped>
    @import url('https://fonts.googleapis.com/css2?family=Nabla&display=swap');
    .wrapper{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 30px;

    }
    h1{
        font-family: "Nabla", system-ui;
        text-align: center;
        font-size: 10em;
    }
    p{
        text-align: center;
        font-size: 18px;
    }
</style>
