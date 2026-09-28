<template>
    <div class="flex flex-col flex-1 overflow-hidden min-w-full sm:min-w-[500px] dark:bg-zinc-950">
        <div class="overflow-y-auto space-y-2 p-2">

            <div class="bg-white dark:bg-zinc-800 rounded shadow">
                <div class="flex border-b border-gray-300 dark:border-zinc-700 text-gray-700 dark:text-gray-200 p-2 font-semibold">Import Paper Message</div>
                <div class="dark:divide-zinc-700 text-gray-900 dark:text-gray-100 p-2 space-y-2">

                    <div class="flex space-x-2">
                        <button @click="pasteFromClipboard" type="button" class="inline-flex items-center rounded-md bg-blue-500 px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm hover:bg-blue-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-500 dark:bg-blue-600 dark:hover:bg-blue-500 dark:focus-visible:outline-blue-600">
                            Paste from Clipboard
                        </button>
                        <button @click="decodePaperMessage" :disabled="!canDecodePaperMessage" type="button" class="inline-flex items-center rounded-md px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2" :class="[ canDecodePaperMessage ? 'bg-blue-500 hover:bg-blue-400 focus-visible:outline-blue-500 dark:bg-blue-600 dark:hover:bg-blue-500 dark:focus-visible:outline-blue-600' : 'bg-gray-400 dark:bg-zinc-500 focus-visible:outline-gray-500 dark:focus-visible:outline-zinc-500 cursor-not-allowed']">
                            <span v-if="isDecodingMessage">Decoding...</span>
                            <span v-else>Decode Paper Message</span>
                        </button>
                    </div>

                    <textarea
                        v-model="paperMessageUri"
                        class="bg-gray-50 border border-gray-300 dark:border-zinc-800 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-zinc-800 dark:text-zinc-100 dark:border-zinc-900"
                        rows="8"
                        placeholder="lxm://"></textarea>

                </div>
            </div>

            <div v-if="decodedMessage" class="bg-white dark:bg-zinc-800 rounded shadow">
                <div class="flex border-b border-gray-300 dark:border-zinc-700 text-gray-700 dark:text-gray-200 p-2 font-semibold">Decoded Paper Message</div>
                <div class="dark:divide-zinc-700 text-gray-900 dark:text-gray-100 p-2 space-y-2">

                    <div>
                        <div class="text-sm font-semibold">Source</div>
                        <div class="text-sm break-all">{{ decodedMessage.source_hash }}</div>
                    </div>

                    <div>
                        <div class="text-sm font-semibold">Destination</div>
                        <div class="text-sm break-all">{{ decodedMessage.destination_hash }}</div>
                    </div>

                    <div v-if="decodedMessage.title">
                        <div class="text-sm font-semibold">Title</div>
                        <div class="text-sm">{{ decodedMessage.title }}</div>
                    </div>

                    <div>
                        <div class="text-sm font-semibold">Message</div>
                        <div class="text-sm whitespace-pre-wrap break-words">{{ decodedMessage.content }}</div>
                    </div>

                    <div class="flex space-x-2">
                        <button @click="addToMessageHistory" :disabled="isAddingToMessageHistory || hasAddedToMessageHistory" type="button" class="inline-flex items-center rounded-md px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2" :class="[ !isAddingToMessageHistory && !hasAddedToMessageHistory ? 'bg-blue-500 hover:bg-blue-400 focus-visible:outline-blue-500 dark:bg-blue-600 dark:hover:bg-blue-500 dark:focus-visible:outline-blue-600' : 'bg-gray-400 dark:bg-zinc-500 focus-visible:outline-gray-500 dark:focus-visible:outline-zinc-500 cursor-not-allowed']">
                            <span v-if="isAddingToMessageHistory">Adding...</span>
                            <span v-else-if="hasAddedToMessageHistory">Added to Message History</span>
                            <span v-else>Add to Message History</span>
                        </button>
                        <button v-if="hasAddedToMessageHistory" @click="openConversation" type="button" class="inline-flex items-center rounded-md bg-blue-500 px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm hover:bg-blue-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-500 dark:bg-blue-600 dark:hover:bg-blue-500 dark:focus-visible:outline-blue-600">
                            Open Conversation
                        </button>
                    </div>

                </div>
            </div>

        </div>
    </div>
</template>

<script>
import DialogUtils from "../../js/DialogUtils";

export default {
    name: 'PaperMessageImportPage',
    data() {
        return {
            paperMessageUri: "",
            decodedMessage: null,
            importedMessage: null,
            isDecodingMessage: false,
            isAddingToMessageHistory: false,
            hasAddedToMessageHistory: false,
        };
    },
    computed: {
        canDecodePaperMessage() {
            return this.paperMessageUri.trim().length > 0 && !this.isDecodingMessage;
        },
    },
    methods: {
        async pasteFromClipboard() {
            try {
                this.paperMessageUri = await navigator.clipboard.readText();
            } catch(e) {
                DialogUtils.alert("Failed to read from clipboard");
                console.log(e);
            }
        },
        async decodePaperMessage() {

            // do nothing if can't decode message
            if(!this.canDecodePaperMessage){
                return;
            }

            this.isDecodingMessage = true;
            this.decodedMessage = null;
            this.importedMessage = null;
            this.hasAddedToMessageHistory = false;

            try {

                // decode lxmf paper message
                const response = await window.axios.post(`/api/v1/lxmf-messages/paper/decode`, {
                    "uri": this.paperMessageUri.trim(),
                });

                this.decodedMessage = response.data;

            } catch(e) {

                // show error
                const message = e.response?.data?.message ?? "Failed to decode paper message";
                DialogUtils.alert(message);
                console.log(e);

            } finally {
                this.isDecodingMessage = false;
            }

        },
        async addToMessageHistory() {

            // Do nothing if no decoded message
            if(!this.decodedMessage || this.isAddingToMessageHistory || this.hasAddedToMessageHistory){
                return;
            }

            this.isAddingToMessageHistory = true;

            try {

                // Add LXMF paper message to message history
                const response = await window.axios.post(`/api/v1/lxmf-messages/paper/import`, {
                    "uri": this.paperMessageUri.trim(),
                });

                this.importedMessage = response.data.lxmf_message;
                this.hasAddedToMessageHistory = true;

            } catch(e) {

                const message = e.response?.data?.message ?? "Failed to add paper message to message history";
                DialogUtils.alert(message);
                console.log(e);

            } finally {
                this.isAddingToMessageHistory = false;
            }

        },
        openConversation() {

            // Do nothing if no imported message
            if(!this.importedMessage){
                return;
            }

            // Open conversation with sender
            this.$router.push({
                name: "messages",
                params: {
                    destinationHash: this.importedMessage.source_hash,
                },
            });

        },
    },
}
</script>
