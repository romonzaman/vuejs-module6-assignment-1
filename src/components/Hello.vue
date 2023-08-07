<!-- 
    Create a simple Vue component that includes an input field and a paragraph. 
    Bind the input field value  using v-model, and display the input's value inside the paragraph. 
    The component should have the following requirements:
    The initial value of the input field should be "Hello". 
    When the user types in the input field, the paragraph should 
    update in real-time to reflect the input value. 
-->
<!--  With Tailwindcss -->

<script setup>
import {ref} from 'vue';

const inputItem = ref('Hello')

</script>


<template>
    <div class="flex flex-col justify-center items-start">
        <div class="flex">
            <label for="inp">Enter Input</label>

            <input v-model="inputItem" 
                type="text" class="ml-5 border-2 border-gray-800" id="inp"/>
        </div>
        <p class="text-xl p-2 bg-gray-200 w-full mt-2">{{ inputItem }}</p>
    </div>
</template>

<style scoped>

</style>
