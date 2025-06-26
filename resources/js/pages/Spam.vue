<script>
// Import layout and Message component
import AppLayout from '../layouts/AppLayout.vue';
import Message from '../components/Message.vue';

export default {
    name: 'Spam',
    layout: AppLayout,
    components: { Message },
    data() {
        return {
            newMessage: '', // Model for input field
            messages: [
                // Initial messages list
                { id: 1, text: 'Cucumber', rated: false, status: null },
                { id: 2, text: 'Keep learning', rated: false, status: null },
            ],
            lastAction: null,   // Tracks last liked/disliked message
            hideRated: false,   // Used for toggling filter
            lastRated: '',      // For debugging/logging
        }
    },
    computed: {
        // Filter messages based on rated status
        filteredMessages() {
            return this.hideRated
                ? this.messages.filter(msg => !msg.rated)
                : this.messages
        }
    },
    methods: {
        // Add a new message to the list
        addMessage() {
            if (!this.newMessage.trim()) return
            this.messages.push({
                id: Date.now(),
                text: this.newMessage,
                rated: false,
                status: null
            })
            this.newMessage = ''
        },
        // Mark message as liked
        likeMessage(msg) {
          msg.status = 'liked'
          msg.rated = true
          this.lastAction = { text: msg.text, type: 'liked' }
        },
        // Mark message as disliked
        dislikeMessage(msg) {
          msg.status = 'disliked'
          msg.rated = true
          this.lastAction = { text: msg.text, type: 'disliked'}
        }
    },

    mounted() {
        // Change footer text on load
        this.$refs.footerText.textContent = "That's all for now =)";
        // Debug log of one of the messages
        console.log(this.$refs["message-1"]);
    },


    watch: {
        // Just logging when a message gets rated
        lastRated(newVal) {
            console.log('Rated message:', newVal)
        }
    }
}
</script>

<template>
    <div class="p-6 font-sans">
        <h1 class="font-bold text-xl mb-3">Spam Board</h1>

        <!-- Input field and buttons -->
        <div class="flex space-x-1 p-6">
            <input
                class="outline-none focus:outline-none"
                v-model="newMessage"
                placeholder="Type your message"
            />
            <button class="bg-white hover:bg-gray-200 text-black px-3 rounded-2xl cursor-pointer"
                    @click="addMessage">Add</button>
            <button class="bg-white hover:bg-gray-200 text-black px-4 rounded-2xl hover:line-through cursor-pointer"
                    @click="hideRated = !hideRated">
                {{ hideRated ? 'Show all' : 'Hide rated' }}
            </button>
        </div>

        <!-- Message list -->
        <div class="mt-4 gap-2 flex flex-col">
            <Message
                v-for="msg in filteredMessages"
                :ref="`message-${msg.id}`"
                :key="msg.id"
                :text="msg.text"
                :status="msg.status"
                @liked="likeMessage(msg)"
                @disliked="dislikeMessage(msg)"
                :rated="msg.rated"
                @mark="markRated(msg)"
            >
                <template #default>
                    <small>– from Spam Board</small>
                </template>
            </Message>
        </div>

        <!-- Display last action -->
        <p v-if="lastAction">
            You {{ lastAction.type }}: <strong>"{{ lastAction.text }}"</strong>
        </p>
        <p ref="footerText" style="margin-top: 2rem; font-weight: bold;"></p>
    </div>
</template>
