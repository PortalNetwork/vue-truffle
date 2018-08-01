<script>
export default {
    data(){
        return {
            web3: null,
            metaMaskId: '1',        // netID 1:正式, 3:測試
            netID: '1',             // 使用者目前的 metamask id
            MetaMaskAddress: "",    // 你的錢包位置
            Message: "",            // 錯誤訊息                             
            MetamaskMsg:{
                LOAD_MATAMASK_WALLET_ERROR: 'Load metamask wallet error, maybe try Metamask later, or upload a wallet json file.',
                EMPTY_METAMASK_ACCOUNT: 'You can choose one MetaMask wallet by unlocking it',
                METAMASK_ACCOUNT: 'You have choosen the MetamMask Wallet: ',
                NETWORK_ERROR: 'Network error, please check it.',
                METAMASK_NOT_INSTALL: 'You must install MetaMask before start.',
                METAMASK_TEST_NET: 'Our game is available on Ropsten Main Network only. Please switch via MetaMask!'
            },
            Web3Interval: null,
            AccountInterval: null,
            NetworkInterval: null,
            stateLog: null,
            isComplete: false,
            type: "Nologin"
        };
    },
    watch:{
        
    },
    methods:{
        fetchWeb3() {
            let web3 = window.web3;
            if (typeof web3 === 'undefined') {
                this.web3 = null;
                this.Log(this.MetamaskMsg.METAMASK_NOT_INSTALL);
            }
        },
        fetchAccounts() {
            if (this.web3 === null) return;
            this.web3.eth.getAccounts((err, accounts) => {
                if (err != null) return this.Log(this.MetamaskMsg.LOAD_MATAMASK_WALLET_ERROR);
                if (accounts.length === 0)  return this.Log(this.MetamaskMsg.EMPTY_METAMASK_ACCOUNT, 'Nologin');
                this.MetaMaskAddress = accounts[0]; //取得使用者的錢包地址
            });
        },
        fetchNetWork() {
            // 要檢查 Network 避免 user 切換錯誤
            this.web3.version.getNetwork((err, netID) => {
                if (err != null) return this.Log(this.MetamaskMsg.METAMASK_TEST_NET);
                if( this.MetaMaskAddress !== '' && this.metaMaskId !== netID) return this.Log(this.MetamaskMsg.METAMASK_TEST_NET, 'NoMainNet');
                this.netID = netID; //取得目前使用者的Network
            })
        },
        Log(msg, type=""){
            this.Message = msg;
            this.$emit("onComplete", {msg});
        }
    },
    mounted(){
        let web3 = window.web3;
        if (typeof web3 !== 'undefined') {
            window.web3 = new Web3(web3.currentProvider);
            this.web3 = window.web3;
            this.fetchAccounts();
            this.fetchNetWork();
            this.Web3Interval = setInterval(() => this.fetchWeb3(), 1000);
            this.AccountInterval = setInterval(() => this.fetchAccounts(), 1000);
            this.NetworkInterval = setInterval(()=>this.fetchNetWork(), 1000);
        } else {
            this.web3 = null;
            this.Log(this.MetamaskMsg.METAMASK_NOT_INSTALL);
        }
    }
};
</script>

<template>
    <div></div>
</template>

<style lang='scss' scoped>

</style>
