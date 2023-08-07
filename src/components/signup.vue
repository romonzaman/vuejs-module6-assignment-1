<script setup>
import { reactive } from 'vue';

const emit = defineEmits(['funcSignup', 'funcChange'])

const form = reactive({
    email: '',
    password: '',
    confirm_password: ''
})
const formError = reactive({
    email: false,
    password: false,
    confirm_password: false
})

const signupHandler = ()=>{
    console.log(form)

    if (form.email == '') {
        formError.email=true
    }else {
        formError.email=false
    }
    if (form.password == '') {
        formError.password=true
    } else {
        formError.password=false
    }
    if (form.password != form.confirm_password){
        formError.confirm_password = true
    } else {
        formError.confirm_password = false
    }

    if( formError.email || formError.password || formError.confirm_password) return

    emit('funcSignup', form)
}

</script>


<template>

    <div class="">
        <div class="w-full flex flex-col bg-blue-100 h-screen  justify-start items-center">
            <div class="flex flex-col justify-center items-center">
                <img src="/draw2.svg" alt="" class="h-64 w-64 m-5 rounded-full bg-blue-200">
                <h1 class="text-4xl mb-5">Registration</h1>
            </div>
            <div class="w-3/4 max-w-lg flex justify-center items-start">
                <form @submit.prevent="signupHandler" action="" class="border-2 w-full rounded-md p-10 bg-white">

                    <div class="flex flex-col justify-start items-start">

                        <label for="email" class="text-lg">Email</label>
                        <input v-model="form.email" type="email" id="email" class="rounded-lg w-full">
                        <span class="error text-xs italic text-red-600" :class="formError.email?'':'hidden'">* Required</span>

                    </div>

                    <div class="flex flex-col justify-start items-start mt-5">

                        <label for="password" class="text-lg">Password</label>
                        <input v-model="form.password" type="password" id="password" class="rounded-lg w-full">
                        <span class="error text-xs italic text-red-600" :class="formError.password?'':'hidden'">* Required</span>

                    </div>

                    <div class="flex flex-col justify-start items-start mt-5">

                        <label for="confirm_password" class="text-lg">Confirm Password</label>
                        <input v-model="form.confirm_password" type="password" id="confirm_password" class="rounded-lg w-full">
                        <span class="error text-xs italic text-red-600" :class="formError.confirm_password?'':'hidden'">* Does not match</span>

                    </div>

                    <div class="flex justify-start items-start mt-5">
                        <button class="p-2 bg-purple-400 rounded-md hover:bg-purple-900 hover:text-white">Signup</button>
                        <button class="p-2 bg-gray-200 rounded-md mx-5 hover:bg-gray-700 hover:text-white" @click.prevent="$emit('funcChange')">Cancel</button>
                    </div>
                    <div>
                        <span class="text-xs text-gray-500">Already Have account? click to <a @click.prevent="$emit('funcChange')" href="#" class="text-blue-500 hover:bg-blue-800 hover:text-white">Login</a></span>
                    </div>

                </form>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
