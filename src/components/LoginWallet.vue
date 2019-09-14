<template>
            <div>
            <div>Login</div>
            <div>Criar Conta</div>
                <div>
                    <input 
                        type="password" 
                        placeholder="Senha (opcional)"
                        v-model="createPassword"
                    />
                    <div @click="createWallet()">Criar</div>
                </div>
            <div>Abrir Conta</div>
            <div>
                <div >Minemonico:</div>
                <textarea 
                    v-model="mnemonic"
                />
                <input 
                    type="password" 
                    placeholder="Senha (opcional)"
                    v-model="password"
                />
                <div
                    @click="login()">Abrir</div>
            </div>
            </div>
</template>

<script>
export default {
    data() {
        return {
            mnemonic: "",
            password: "",
            createPassword: ""
        }
    },
    methods: {
        createWallet(){
            this.$emit("hasCreated" , this.createPassword)
        },

        login(){
            this.$emit("hasLogin" , [this.mnemonic, this.password])
        }   
    
    }
}
</script>

<style>
</style>
