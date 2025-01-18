<template lang="">
    <div >
        <header class="flex items-center gap-2 p-4 ">
            <div class="flex items-center gap-2 hover:scale-[105%] transition cursor-pointer"> 
                <Logo/>
                <p class="font-bold">Daspor</p>
            </div>

        </header>
        <div class="px-4 grow">
            <div class="grid gap-4">
                <div v-for='(item, index) in items' :key='index' 
                class="flex items-center gap-2 px-3 py-1 hover:bg-neutral-100 rounded-lg transition cursor-pointer">
                <Icon :name="item.icon" color="black" size="20" />
                    <span class="material-icons">{{ item.title }}</span>
                </div>            
            </div>
        </div>  
    </div>
</template>
<script setup>
const items =ref([
{
        title: 'Dashboard',
        icon: 'ic:outline-dashboard',
        path: '/dashboard'
    },
    {
        title: 'Header',
        icon: 'mdi:head-cog-outline',
        path: '/header'
    },
    {
        title: 'About Me',
        icon: 'cib:about-me',
        path: '/aboutme'
    },
    {
        title: 'Service',
        icon: 'hugeicons:service',
        path: '/service'
    },
    {
        title: 'Projects',
        icon: 'eos-icons:project-outlined',
        path: '/projects'
    },
    {
        title: 'Review',
        icon: 'material-symbols:category-search-outline',
        path: '/review'
    },
    {
        title: 'FAQs',
        icon: 'mdi:faq',
        path: '/faqs'
    },
    {
        title: 'Reach me!',
        icon: 'simple-line-icons:call-in',
        path: '/reachme'
    },
])
</script>
<style lang="">
    
</style>