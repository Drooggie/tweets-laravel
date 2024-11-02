<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import Tweet from '@/Components/Tweet.vue';
import InputError from '@/Components/InputError.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import { useForm, Head } from '@inertiajs/vue3';

defineProps(['tweets'])

const form = useForm({
    message: '',
})
</script>

<template>
    <Head title="Tweets" />

    <AuthenticatedLayout>
        <div class="max-w-2xl mx-auto p-4 sm:p-6 lg:p-8">
            <form @submit.prevent="form.post(route('tweets.store'), {onSuccess: () => form.reset()})">
                <textarea 
                    v-model="form.message"
                    placeholder="Place to tweet"
                    class="block w-full border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm bg-black text-white placeholder-white"
                    >
                </textarea>
                <InputError :message="form.errors.message" class="mt-2"/>
                <PrimaryButton class="mt-4">Tweet</PrimaryButton>
            </form>

            <div class="mt-6 bg-black shadow-sm rounded-lg divide-y">
                <Tweet
                    v-for="tweet in tweets"
                    :key="tweet.id"
                    :tweet="tweet"
                />
            </div>


        </div>
    </AuthenticatedLayout>

</template>