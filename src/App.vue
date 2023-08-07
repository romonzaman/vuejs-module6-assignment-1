<script setup>
import { ref, reactive } from 'vue';

import signup from './components/signup.vue'
import login from './components/login.vue'
import welcome from './components/welcome.vue'

const loggedIn = ref(false)
const isRegister = ref(true)


//default login
const userData = reactive({
    email: 'romon.zaman@gmail.com',
    password: '123456'
})

const funcSignupSuccess = (form)=>{
    userData.email=form.email
    userData.password=form.password
    console.log(userData)
    isRegister.value = false
}

const logoutFunc = ()=>{
    loggedIn.value = false
    isRegister.value = false
}
</script>

<template>
    <template v-if="loggedIn">
        <welcome @func-logout="logoutFunc()" />
    </template>

    <template v-else>
        <signup @func-change="()=>isRegister=false" @func-signup="funcSignupSuccess" v-if="isRegister" />

        <login  @func-change="()=>isRegister=true" @func-login="()=>loggedIn=true" :logindata="userData"  v-else  />
    </template>
</template>

<style scoped></style>
