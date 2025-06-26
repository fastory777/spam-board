<script>
import { HandThumbDownIcon } from '@heroicons/vue/24/outline';
import { HandThumbUpIcon } from '@heroicons/vue/24/outline';


export default {
    components: {
        HandThumbDownIcon,
        HandThumbUpIcon,
    },
    props: {
        name: 'Message',
        text: String,
        used: Boolean
    },
    data() {
        return {
            color: "black",
        }
    },
    emits: ['mark'],
    computed: {
        isLong() {
            return this.text.length > 20
        },
    },
    methods: {
        changeColor(color = "blue") {
            this.color = color;
        }
    },
    mounted() {
        console.log(this.text)
    }
}
</script>

<template>
    <div>
        <div class="flex space-x-1">
            <p class="mb-1 font-medium">{{ text }}</p>
            <hand-thumb-up-icon class="w-5 h-5 text-green-500 hover:text-green-700 cursor-pointer" v-if="!used" @click="$emit('mark')"></hand-thumb-up-icon>
            <hand-thumb-down-icon class="w-5 h-5 text-red-500 hover:text-red-700 cursor-pointer" v-if="!used" @click="$emit('mark')"></hand-thumb-down-icon>
        </div>

        <slot />
    </div>
</template>
