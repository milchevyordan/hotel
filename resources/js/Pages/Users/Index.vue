<script setup lang="ts">
import { Head, Link } from '@inertiajs/vue3';

import Table from '@/DataTable/Table.vue';
import { DataTable } from '@/DataTable/types';
import IconPencilSquare from '@/Icons/PencilSquare.vue';
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { User } from '@/types';
import { dateTimeToLocaleString } from '@/utils';

defineProps<{
    dataTable: DataTable<User>;
}>();
</script>

<template>
    <Head :title="'User'" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800 dark:text-gray-200"
            >
                User
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="bg-white shadow-sm sm:rounded-lg dark:bg-gray-800">
                    <div class="p-6 text-gray-900 dark:text-gray-100">
                        <Table
                            :data-table="dataTable"
                            :per-page-options="[5, 10, 15, 20, 50]"
                            :global-search="true"
                            :advanced-filters="false"
                        >
                            <template #additionalContent>
                                <div class="flex w-full gap-2">
                                    <Link
                                        class="w-full rounded-md border border-gray-300 px-5 py-1.5 transition hover:bg-gray-50 active:scale-95 md:w-auto dark:border-gray-700 dark:hover:bg-gray-800"
                                        :href="route('users.create')"
                                    >
                                        Create User
                                    </Link>
                                </div>
                            </template>

                            <template #cell(created_at)="{ value, item }">
                                <div class="flex gap-1.5">
                                    {{ dateTimeToLocaleString(value) }}
                                </div>
                            </template>

                            <template #cell(action)="{ value, item }">
                                <div class="flex gap-1.5">
                                    <Link
                                        class="rounded-md border border-gray-300 p-1 transition active:scale-90 dark:border-gray-700"
                                        :title="'Edit User'"
                                        :href="route('users.edit', item.id)"
                                    >
                                        <IconPencilSquare
                                            classes="w-4 h-4 text-[#909090]"
                                        />
                                    </Link>
                                </div>
                            </template>
                        </Table>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
