<script>
import AppLayout from '../layouts/AppLayout.vue';
import Message from '../components/Message.vue';

export default {
    name: 'Spam',
    layout: AppLayout,
    components: { Message },
    data() {
        return {
            newMessage: '',
            messages: [
                { id: 1, text: 'Cucumber', used: false },
                { id: 2, text: 'Keep learning', used: false }
            ],
            hideUsed: false,
            lastUsed: '',
        }
    },
    computed: {
        filteredMessages() {
            return this.hideUsed
                ? this.messages.filter(msg => !msg.used)
                : this.messages
        }
    },
    methods: {
        addMessage() {
            if (!this.newMessage.trim()) return
            this.messages.push({
                id: Date.now(),
                text: this.newMessage,
                used: false
            })
            this.newMessage = ''
        },
        markUsed(msg) {
            msg.used = true
            this.lastUsed = msg.text
        }
    },

    mounted() {
        this.$refs.footerText.textContent = "That's all for now =)";
        console.log(this.$refs["message-1"]);
    },


    watch: {
        lastUsed(newVal) {
            console.log('Used message:', newVal)
        }
    }
}
</script>

<template>
    <div class="p-6 font-sans">
        <h1 class="font-bold text-xl mb-3">Spam Board</h1>
        <div class="flex space-x-1 p-6">
            <input class="outline-none focus:outline-none" v-model="newMessage" placeholder="Type your message" />
            <button class="bg-white hover:bg-gray-200 text-black px-3 rounded-2xl cursor-pointer" @click="addMessage">Add</button>
            <button class="bg-white hover:bg-gray-200 text-black px-4 rounded-2xl hover:line-through cursor-pointer" @click="hideUsed = !hideUsed">
                {{ hideUsed ? 'Show all' : 'Hide rated' }}
            </button>
        </div>


        <div class="mt-4 gap-2 flex flex-col">
            <Message
                v-for="msg in filteredMessages"
                :ref="`message-${msg.id}`"
                :key="msg.id"
                :text="msg.text"
                :used="msg.used"
                @mark="markUsed(msg)"
            >
                <template #default>
                    <small>– from Spam Board</small>
                </template>
            </Message>
        </div>

        <p v-if="lastUsed">Last disliked message: <strong>{{ lastUsed }}</strong></p>
        <p ref="footerText" style="margin-top: 2rem; font-weight: bold;"></p>
    </div>
</template>
