<script setup>
import { ref, reactive } from 'vue';

const props = defineProps({
    logindata: {
        type: Object
    }
})

const emit = defineEmits(['funcLogin', 'funcChange'])

const loading = ref(false)
const btnDisabled = ref(false)
const loginFailed = ref(false)

const form = reactive({
    email: '',
    password: ''
})
const formError = reactive({
    email: false,
    password: false
})

//function - validate required, check login data
const loginHandler = () => {
    loginFailed.value=false
    if (form.email == '') {
        formError.email = true
    } else {
        formError.email = false
    }
    if (form.password == '') {
        formError.password = true
    } else {
        formError.password = false
    }
    if (formError.email || formError.password) return

    if (form.email != props.logindata.email || form.password!=props.logindata.password){
        loginFailed.value=true
        return
    }

    btnDisabled.value = true
    loading.value = true
    loginFailed.value=false

    // simulate api execution delay
    setTimeout(()=>{
        loading.value = false
        emit('funcLogin', form)
    },1000)
    
}

</script>


<template>
    <div class="">
        <div class="w-full flex flex-col bg-blue-100 h-screen  justify-start items-center">
            <div class="flex flex-col justify-center items-center">
                <img src="/logo.png" alt="" class="h-64 w-64 m-5 rounded-full bg-blue-200 opacity-50">
                <h1 class="text-4xl mb-5">Login</h1>

                <div role="status" class="mt-7" :class="loading?'':'hidden'">
                    <svg aria-hidden="true" class="w-8 h-8 mr-2 text-gray-200 animate-spin dark:text-gray-600 fill-blue-600"
                        viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                            fill="currentColor" />
                        <path
                            d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                            fill="currentFill" />
                    </svg>
                    <span class="sr-only">Loading...</span>
                </div>
                <div class="error pt-5 text-red-600 text-xs italic font-bold"
                    :class="loginFailed?'':'hidden'" 
                >Username and password are incorrect. please try again</div>
            </div>
            <div class="h-1/2 w-3/4 max-w-lg flex justify-center items-start">
                <form @submit.prevent="loginHandler" action="" class="border-2 w-full rounded-md px-10 py-10 bg-white">

                    <div class="flex flex-col justify-start items-start">

                        <label for="email" class="text-lg">Email</label>
                        <input v-model="form.email" type="email" class="rounded-lg w-full">
                        <span class="error text-xs italic text-red-600" :class="formError.email ? '' : 'hidden'">*
                            Required</span>
                    </div>

                    <div class="flex flex-col justify-start items-start mt-5">

                        <label for="password" class="text-lg">Password</label>
                        <input v-model="form.password" type="password" class="rounded-lg w-full">
                        <span class="error text-xs italic text-red-600" :class="formError.password ? '' : 'hidden'">*
                            Required</span>

                    </div>

                    <div class="flex justify-start items-start mt-5">
                        <button class="p-2 bg-purple-400 rounded-md hover:bg-purple-900 hover:text-white"
                            type="submit" :disabled="btnDisabled">Login</button>
                    </div>
                    <div>
                        <span class="text-xs text-gray-500">Don't Have account? click to <a @click.prevent="$emit('funcChange')"
                                href="#" class="text-blue-500 hover:bg-blue-800 hover:text-white">Signup</a></span>
                    </div>
            </form>
        </div>
    </div>
</div></template>

<style scoped></style>
