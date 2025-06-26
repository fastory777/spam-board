<script setup>
import { router, Link, Head } from '@inertiajs/vue3'


</script>

<template>
    <Head title="Welcome" />

    <div class="w-64 h-64 bg-red-400">
        Hello
    </div>

    <Link class="text-black" href="/spam-board">start spamming</Link>
</template>
