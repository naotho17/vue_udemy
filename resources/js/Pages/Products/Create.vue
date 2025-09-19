<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import SelectInput from '@/Components/SelectInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const taxs = [{id:10,name:'10%'},{id:8,name:'8%'},{id:0,name:'非課税'}]

const form = useForm({
    name: '',
    code: '',
    price: '',
    tax: '',
});

const submit = () => {
    form.post(route('products.store'), {
        //onSuccess:データが入力された場合のみフォームリセット
        onSuccess: () => form.reset('name', 'code','price','tax'),
        // onFinishにすると送信処理後必ず実行される
        // onFinish: () => form.reset('name', 'code','price','tax'),
    });
};
</script>

<template>
    <Head title="商品登録" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800"
            >
                商品登録
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div
                    class="overflow-hidden bg-white shadow-sm sm:rounded-lg"
                >
                    <div class="p-6 text-gray-900">
                        商品登録
                    </div>
                    <form @submit.prevent="submit">
                        <div class="mt-4">
                            <InputLabel for="name" value="Name" />

                            <TextInput
                            id="name"
                            type="text"
                            class="mt-1 block w-full"
                            v-model="form.name"
                            required
                            autofocus
                            autocomplete="name"
                            />

                            <InputError class="mt-2" :message="form.errors.name" />
                        </div>
                        <div class="mt-4">
                            <InputLabel for="code" value="Code" />
                            <TextInput
                                id="code"
                                type="text"
                                class="mt-1 block w-full"
                                v-model="form.code"
                                required
                                autocomplete="code"
                            />
                            <InputError class="mt-2" :message="form.errors.code" />
                        </div>
                        <div class="mt-4">
                            <InputLabel for="price" value="Price" />
                            <TextInput
                                id="price"
                                type="text"
                                class="mt-1 block w-full"
                                v-model="form.price"
                                required
                                autocomplete="price"
                            />
                            <InputError class="mt-2" :message="form.errors.price" />
                        </div>

                        <div class="mt-4">
                            <InputLabel for="tax" value="Tax" />
                            <SelectInput :options="taxs"
                                id="tax"
                                class="mt-1 block w-full"
                                v-model="form.tax"
                                required
                                autocomplete="tax"
                            />
                            <InputError class="mt-2" :message="form.errors.tax" />
                        </div>              

                        <div class="flex items-center justify-end mt-4">

                            <PrimaryButton class="ms-4" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                                登録
                            </PrimaryButton>
                        </div>                        
                    </form>
                
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
