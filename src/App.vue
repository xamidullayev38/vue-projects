<script>

    import Input from './components/Input.vue';
    import Selector from './components/Selector.vue';
    import CryptoConvert from 'crypto-convert';
    import Favourite from './components/Favourite.vue';
    const convert = new CryptoConvert();
    export default{
        components: { Input, Selector, Favourite },
        data () {
            return{
                amount: 0,
                cryptoFirst: '',
                cryptoSecond: '',
                error: '',
                result: 0,
                favs: []
            }
        },
        methods: {
            getFromFavs(index){
                this.cryptoFirst = this.favs[index].from
                this.cryptoSecond = this.favs[index].to
            },
            getFavs() {
                const alreadyExists = this.favs.some(fav => fav.from === this.cryptoFirst && fav.to === this.cryptoSecond );
                if(!this.cryptoFirst || !this.cryptoSecond) {
                    alert('Choose conversion')
                    return
                }
                if (alreadyExists) {
                    alert('this conversion is already existed!')
                    return
                }
                if (this.cryptoFirst == this.cryptoSecond) {
                    alert('The currencies are same') 
                    return
                }
                this.favs.push(
                    {
                        from: this.cryptoFirst,
                        to: this.cryptoSecond
                    }
                )
            },
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
                    alert('Enter number upper than zero')
                    return 
                }else if (this.cryptoFirst == '' || this.cryptoSecond == ''){
                    alert('Chose currency')
                    return
                } else if (this.cryptoFirst == this.cryptoSecond){
                    alert('Enter different currency')
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
        <Input :getFavs="getFavs" :changeAmount="changeAmount" :convert="convert"/>
        <p v-if="result !== 0" class="result-text">{{ result }} </p>
        <Favourite v-if="favs.length > 0" :getFromFavs="getFromFavs" :favs="favs" />
        <div class="selectors">
            <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
            <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
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
