<template>
    <div>
    <div v-if="{logged: false}">
        <LoginWallet @hasCreated="createWallet" @hasLogin="openWallet" />
        <div></div>
    </div>
    <div v-else>
        eai
    </div>
    </div>
</template>

<script>
import {generateMnemonic, mnemonicToSeed} from  "bip39"
import hdkey from "hdkey"
import {privateToPublic, publicToAddress, toChecksumAddress} from "ethereumjs-util"

import LoginWallet from "./LoginWallet"

export default {
    components:{
       'LoginWallet': LoginWallet
    },
    data() {
        return {
            logged: false,
        }
    },
    methods: {
        async openWallet(mnemonic, password){
        const seed = await mnemonicToSeed(mnemonic, password || "");

        const root = hdkey.fromMasterSeed(seed);
        // const masterPrivateKey = root.privateKey.toString('hex');

        const addrNode = root.derive("m/44'/60'/0'/0/0");
        const pubKey = privateToPublic(addrNode._privateKey);
        const addr = publicToAddress(pubKey).toString('hex');
        const address = toChecksumAddress(addr);
       
        console.log(address)
      },
        async createWallet(password){
        const mnemonic = await generateMnemonic();
        const seed = await mnemonicToSeed(mnemonic, password || "");

        const root = hdkey.fromMasterSeed(seed);
        // const masterPrivateKey = root.privateKey.toString('hex');

        const addrNode = root.derive("m/44'/60'/0'/0/0");
        const pubKey = privateToPublic(addrNode._privateKey);
        const addr = publicToAddress(pubKey).toString('hex');
        const address = toChecksumAddress(addr);

        console.log(mnemonic, address)
      }
   }
}
</script>

<style>
</style>
