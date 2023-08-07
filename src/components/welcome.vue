<script setup>
import { reactive } from 'vue';

const form = reactive({
    email: '',
    password: '',
    confirm_password: ''
})

const emit = defineEmits(['funcLogout'])

const logoutHandler = ()=>{
    emit('funcLogout')
}

</script>


<template>

    <div class="">
        <div class="w-full flex flex-col bg-blue-100 h-screen  justify-center items-center">
            <div class="h-1/2 flex justify-center items-end">
                <img src="/draw2.svg" alt="" class="h-64 w-64 m-5 rounded-full bg-blue-200">
            </div>
            <div class="h-1/2 w-3/4 max-w-lg flex flex-col justify-start items-center">
                <div class="flex justify-center items-center bg-white w-full p-5">
                    <h1>Welcome</h1>
                </div>
                <div class="flex justify-center items-center w-full">
                    <a @click.prevent="logoutHandler()" href="" class="p-1 text-xs text-blue-500 hover:text-blue-50 hover:bg-blue-700">Logout</a>
                </div>

            </div>
        </div>
    </div>



</template>

<style scoped></style>
