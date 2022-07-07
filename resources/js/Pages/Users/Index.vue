<script>
// import AppLayout from '@/Layouts/AppLayout.vue';
import {Inertia} from "@inertiajs/inertia";
import {InertiaLink} from '@inertiajs/inertia-vue3';
import JetButton from '@/Jetstream/Button.vue';
import JetInput from '@/Jetstream/Input.vue';
import ConfirmationModal from "@/Jetstream/ConfirmationModal.vue";
import {ref} from "vue";
import AdminLayout from "../AdminLayout.vue";

export default {
    props: ["users"],
    components: {
        AdminLayout,
        InertiaLink, JetButton, JetInput, ConfirmationModal,
    },
    setup() {
        const showModal = ref(false)
        const selectedUser = ref({})

        const destroy = () => {
            Inertia.delete(route('user.destroy', { customer: selectedUser.value.id }))
            showModal.value = false
        }

        return { showModal, selectedUser, destroy }
    }
}
</script>

<template>
    <AdminLayout>
        <template #content>
            <InertiaLink :href="route('user.create')">
                <JetButton class="mb-3">Create</JetButton>
            </InertiaLink>
            <div class="bg-white overflow-auto shadow-xl sm:rounded-lg md:none">
                <table class="w-full text-sm text-left text-gray-500">
                    <thead class="text-xs text-gray-700 uppercase bg-gray-50 ">
                    <tr>
                        <th scope="col" class="px-6 py-3">
                            #
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Nombre
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Correo
                        </th>
                        <th scope="col" class="px-6 py-3">
                            Acciones
                        </th>
                    </tr>
                    </thead>
                    <tbody v-for="user in users" :key="user.id">
                    <tr class="bg-white border-b hover:bg-gray-50 ">
                        <th scope="row"
                            class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap">
                            {{ user.id }}
                        </th>
                        <td class="px-6 py-4">
                            {{ user.name }}
                        </td>
                        <td class="px-6 py-4">
                            {{ user.email }}
                        </td>
                        <td class="flex px-6 py-4 text-center">
                            <InertiaLink
                                :href="route('user.edit', { customer: user })"
                                class="font-medium text-blue-600">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
                                     viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                          d="M15.232 5.232l3.536 3.536m-2.036-5.036a2.5 2.5 0 113.536 3.536L6.5 21.036H3v-3.572L16.732 3.732z"/>
                                </svg>
                            </InertiaLink>
                            <a
                                @click="showModal = true;selectedUser = user"
                                class="font-medium cursor-pointer text-red-500 ml-2">
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none"
                                     viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                                    <path stroke-linecap="round" stroke-linejoin="round"
                                          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                                </svg>
                            </a>
                        </td>
                    </tr>
                    </tbody>
                </table>
                <confirmation-modal :show="showModal">
                    <template #title>Borrar Usuario</template>
                    <template #content v-if="selectedUser">Estas seguro de borrar el usuario {{
                            selectedUser.name
                        }}
                    </template>
                    <template #footer>
                        <jet-button @click.prevent="showModal = false">Cerrar</jet-button>
                        <jet-button @click="destroy" class="bg-red-500 ml-2">Borrar</jet-button>
                    </template>
                </confirmation-modal>
            </div>
        </template>
    </AdminLayout>
</template>
