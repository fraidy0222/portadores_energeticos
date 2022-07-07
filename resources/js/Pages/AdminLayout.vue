<script setup>
import {ref} from "vue";
import Sidebar from '@/components/Sidebar.vue';
import Navbar from '@/components/NavbarComponent.vue';
import {MenuAlt1Icon} from '@heroicons/vue/outline';
import JetNavLink from '@/Jetstream/NavLink.vue';

const sidebarShow = ref(false)

</script>

<template>
    <div class="flex flex-no-wrap bg-gray-200">
        <Sidebar :sidebarShow="sidebarShow"/>
        <div class="flex-1">
            <Navbar>
                <button
                    @click="sidebarShow = !sidebarShow"
                    class="flex items-center sm:hidden justify-center p-0.5 rounded bg-gray-800 focus:outline-none focus:ring-1 focus:ring-gray-500"
                >
                    <MenuAlt1Icon class="w-5 h-5 text-white"/>
                </button>
            </Navbar>

            <div class="container mx-auto py-10 w-11/12 min-h-screen">
                <!-- Place your content here -->
                <slot name="content"></slot>
            </div>
        </div>
    </div>
</template>
