<script>
// Importing icons from Heroicons library
import { HandThumbDownIcon } from '@heroicons/vue/24/outline';
import { HandThumbUpIcon } from '@heroicons/vue/24/outline';


export default {
    components: {
        HandThumbDownIcon,
        HandThumbUpIcon,
    },
    props: {
        // Props coming from parent component
        name: 'Message',
        text: String,
        rated: Boolean,
        status: String,
    },
    data() {
        return {
            // Just an example color, not used here (at least now =)
            color: "black",
        }
    },
    emits: ['mark', 'liked', 'disliked'], // Declare emitted events
    computed: {
        // Unused helper to check if text is long, is not used right now
        isLong() {
            return this.text.length > 20
        },
    },
    methods: {
        // Unused method to change color (at least now =)
        changeColor(color = "blue") {
            this.color = color;
        }
    },
    mounted() {
        // Just console logging message text for debugging
        console.log(this.text)
    }
}
</script>

<template>
    <div>
        <div class="flex space-x-1">
            <p class="mb-1 font-medium">{{ text }}</p>

            <!-- Thumbs up icon (like) -->
            <hand-thumb-up-icon
                class="w-5 h-5 text-green-500 hover:text-green-700 cursor-pointer"
                v-if="!rated && status === null"
                @click="$emit('liked')"
            ></hand-thumb-up-icon>

            <!-- Thumbs down icon (dislike) -->
            <hand-thumb-down-icon
                class="w-5 h-5 text-red-500 hover:text-red-700 cursor-pointer"
                v-if="!rated && status === null"
                @click="$emit('disliked')"
            ></hand-thumb-down-icon>
        </div>

        <!-- Default slot, used for footer text -->
        <slot />
    </div>
</template>
