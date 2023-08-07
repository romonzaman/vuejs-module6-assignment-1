<script setup>
import { ref, reactive } from 'vue';

import signup from './components/signup.vue'
import login from './components/login.vue'
import welcome from './components/welcome.vue'

const loggedIn = ref(false)

const isRegister = ref(true)

const funcSignup = () => {
    isRegister.value = true
}
const funcLogin = () => {
    isRegister.value = false
}

const userData = reactive({
    email: 'romon.zaman@gmail.com',
    password: '123456'
})
const funcLoginHandler = (form)=>{
    console.log(form)
    if (form.email == userData.email && form.password==userData.password){
        loggedIn.value = true
    } else {
        loggedIn.value = false
    }
}
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
        <signup :func-change="funcLogin" @func-signup="funcSignupSuccess" v-if="isRegister" />
        <login :func-change="funcSignup" @func-login="funcLoginHandler" v-else  />
    </template>
</template>

<style scoped></style>
