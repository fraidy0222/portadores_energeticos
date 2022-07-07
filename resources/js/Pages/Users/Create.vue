<script>
import { InertiaLink,useForm } from '@inertiajs/inertia-vue3';
import JetButton from '@/Jetstream/Button.vue';
import JetInputError from '@/Jetstream/InputError.vue';
import AdminLayout from "../AdminLayout.vue";

export default {
    components: {

        AdminLayout, JetButton, JetInputError, InertiaLink
    },
    props: {
        errors: Object
    },
    setup() {
        const form = useForm({
            name: '',
            email: '',
            password: ''
        })
        return { form }
    }
}

</script>

<template>
    <AdminLayout>
        <template #content>
            <section class="max-w-6xl p-6 mx-auto bg-white rounded-md shadow-md">
                <h2 class="text-lg font-semibold text-gray-700 capitalize dark:text-white">User Create</h2>
                <form @submit.prevent="form.post(route('user.store'))">
                    <div class="grid grid-cols-1 gap-6 mt-4">
                        <div>
                            <label class="text-gray-700 " for="name">Name</label>
                            <input id="name" type="text"
                                   v-model="form.name"
                                   class="block w-full px-4 py-2 mt-2 text-gray-700 bg-white border border-gray-200 rounded-md  focus:border-blue-400 focus:ring-blue-300 focus:ring-opacity-40 focus:outline-none focus:ring">
                            <JetInputError :message="errors.name" class="mt-2"/>
                        </div>

                        <div>
                            <label class="text-gray-700 " for="email">Email</label>
                            <input id="email" type="text"
                                   v-model="form.email"
                                   class="block w-full px-4 py-2 mt-2 text-gray-700 bg-white border border-gray-200 rounded-md  focus:border-blue-400 focus:ring-blue-300 focus:ring-opacity-40 focus:outline-none focus:ring">
                            <JetInputError :message="errors.email" class="mt-2"/>
                        </div>
                        <div>
                            <label class="text-gray-700 " for="password">Password</label>
                            <input id="password" type="password"
                                   v-model="form.password"
                                   class="block w-full px-4 py-2 mt-2 text-gray-700 bg-white border border-gray-200 rounded-md  focus:border-blue-400 focus:ring-blue-300 focus:ring-opacity-40 focus:outline-none focus:ring">
                            <JetInputError :message="errors.password" class="mt-2"/>
                        </div>
                    </div>

                    <div class="flex justify-end mt-6">
                        <JetButton type="submit" class="mr-3" :class="{'opacity-25 cursor-not-allowed': form.processing}"
                                   :disable="form.processing">Save
                        </JetButton>
                        <InertiaLink :href="route('user.index')">
                            <JetButton>Cancel</JetButton>
                        </InertiaLink>
                    </div>
                </form>
            </section>
        </template>
    </AdminLayout>
</template>
