<template lang="">
    <div class="">
        <div class="z-50 flex lg:hidden bg-green-500 items-center justify-between p-4 w-full h-full">
            <Logo/>
            <Icon class="z-50 cursor-pointer left-2 top-2" 
            size="30" 
            name="cil:burger" @click="open = true"/>

            <div v-if="open" class="absolute 
            top-0 left-0 z-[999] bg-white w-full h-full h-screen">
            <Icon class=" absolute z-50 cursor-pointer right-6 top-6" 
            size="30" 
            name="material-symbols:close" @click="open = false"/>

                <SidebarMenu/>
            </div>
        </div>

        <div class="hidden lg:flex bg-red-500 w-[250px] h-screen flex flex-col justify-between border-r">
            <SidebarMenu/>
            <div>
            User Menu
        </div>
        </div>

    </div>
</template>
<script setup>
const open = ref(false)
console.log(open)
</script>