<script setup>
import { Link } from "@inertiajs/inertia-vue3";
import {ref} from "vue";
import {
    LightBulbIcon,
    UserIcon, KeyIcon,
    ChartSquareBarIcon,
    ClipboardListIcon,
    CurrencyDollarIcon,
    TruckIcon,
    IdentificationIcon,
    MenuAlt1Icon
} from '@heroicons/vue/outline';

const props = defineProps({
    sidebarShow: {
        type: Boolean
    }
})

const admin = [
    {title: 'Users', icon: UserIcon, link: route('user.index')},
    {title: 'Roles', icon: KeyIcon},
    {title: 'Dependencias', icon: KeyIcon},
    {title: 'Nivel de Actividad', icon: ChartSquareBarIcon},
    {title: 'Portadores', icon: LightBulbIcon},
    {title: 'Planes', icon: ClipboardListIcon},
    {title: 'Asignacion Mensual', icon: CurrencyDollarIcon},
    {title: 'Pruebas de Litro'},
    {title: 'Equipo', icon: TruckIcon,},
    {title: 'Operador', icon: IdentificationIcon},
]
const subMenu = [
    {
        title: 'Consumo', icon: IdentificationIcon,
        child: [
            {text: 'Metros Contadores'},
            {text: '5%'},
            {text: 'Líquidos asfálticos'},
        ]
    }
]
</script>
<template>
    <div
        class="w-64 bg-gray-900 absolute inset-y-0 left-0 transform -translate-x-full transition duration-200 ease-in-out md:relative md:-translate-x-0"
        :class="{ 'relative -translate-x-0': sidebarShow }"
    >
        <perfect-scrollbar>
            <div class="px-6 pt-4">
                <!-- Logo -->
                <div class="flex items-center justify-between">
                    <a
                        href="#"
                        class="bg-blue-600 p-1.5 rounded flex items-center justify-center focus:outline-none focus:ring-1 focus:ring-blue-500 focus:ring-offset-2 focus:ring-offset-gray-900"
                    >
                        <svg
                            class="w-5 h-5 text-white stroke-current"
                            viewBox="0 0 24 24"
                            fill="none"
                        >
                            <path
                                d="M12 4.75L19.25 9L12 13.25L4.75 9L12 4.75Z"
                                stroke="currentColor"
                                stroke-width="1.5"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                            ></path>
                            <path
                                d="M9.25 12L4.75 15L12 19.25L19.25 15L14.6722 12"
                                stroke="currentColor"
                                stroke-width="1.5"
                                stroke-linecap="round"
                                stroke-linejoin="round"
                            ></path>
                        </svg>
                    </a>
                </div>
            </div>
            <div class="px-6 pt-4">
                <ul class="flex flex-col space-y-2" v-for="(item, index) in admin" :key="index">
                    <li class="relative text-gray-500 hover:text-white transition duration-200 focus-within:text-white">
                        <div
                            class="absolute inset-y-0 left-0 flex items-center pointer-events-none"
                        >
                            <Component :is="item.icon" class="w-5 h-5"></Component>
                        </div>
                        <Link
                            :href="item.link"
                            class="inline-block w-full py-2 pl-8 pr-4 text-md rounded hover:bg-gray-800 focus:outline-none focus:ring-1 focus:ring-gray-500 focus:bg-gray-800"
                        >{{ item.title }}
                        </Link>
                    </li>
                </ul>
                <ul class="flex flex-col space-y-2" v-for="(item, index) in subMenu" :key="index">
                    <li>
                        <div
                            class="relative flex justify-between items-center text-gray-500 hover:text-white focus-within:text-white"
                        >
                            <div class="flex items-center w-full">
                                <div
                                    class="absolute inset-y-0 left-0 flex items-center pointer-events-none"
                                >
                                    <Component :is="item.icon" class="w-5 h-5"></Component>
                                </div>
                                <a
                                    href="#"
                                    class="inline-block w-full py-2 pl-8 pr-4 text-md rounded hover:bg-gray-800 focus:outline-none focus:ring-1 focus:ring-gray-500 focus:bg-gray-800"
                                >{{ item.title }}</a
                                >
                            </div>
                            <button class="absolute right-0 flex items-center p-1" tabindex="-1">
                                <svg class="w-5 h-5 stroke-current" fill="none" viewBox="0 0 24 24">
                                    <path
                                        stroke="currentColor"
                                        stroke-linecap="round"
                                        stroke-linejoin="round"
                                        stroke-width="1.5"
                                        d="M15.25 10.75L12 14.25L8.75 10.75"
                                    ></path>
                                </svg>
                            </button>
                        </div>
                        <div class="pt-2 pl-4">
                            <ul class="flex flex-col pl-2 text-gray-500 border-l border-gray-700"
                                v-for="(item, index) in item.child" :key="index">
                                <li>
                                    <a
                                        href="#"
                                        class="inline-block w-full px-4 py-1 text-md rounded hover:bg-gray-800 hover:text-white focus:outline-none focus:ring-1 focus:ring-gray-500 focus:text-white"
                                    >{{ item.text }}</a
                                    >
                                </li>
                            </ul>
                        </div>
                    </li>
                </ul>
            </div>
        </perfect-scrollbar>
    </div>
</template>

<style>
.ps{
    height: 100vh;
}
</style>

