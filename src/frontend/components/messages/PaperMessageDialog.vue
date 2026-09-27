<template>
    <div v-if="isShowing" class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity flex items-center justify-center">
        <div class="flex w-full h-full p-4 overflow-y-auto">
            <div v-click-outside="dismiss" class="my-auto mx-auto w-full bg-white dark:bg-zinc-900 rounded-lg shadow-xl max-w-2xl">

                <!-- title -->
                <div class="p-4 border-b dark:border-zinc-700">
                    <h3 class="text-lg font-semibold dark:text-white">LXMF Paper Message</h3>
                </div>

                <!-- content -->
                <div class="p-4">
                    <textarea
                        ref="paper-message-uri"
                        readonly
                        :value="uri"
                        class="bg-gray-50 border border-gray-300 dark:border-zinc-800 text-gray-900 text-sm rounded-lg block w-full p-2.5 dark:bg-zinc-800 dark:text-zinc-100 dark:border-zinc-900"
                        rows="8"></textarea>
                </div>

                <!-- actions -->
                <div class="p-4 border-t dark:border-zinc-700 flex justify-end space-x-2">
                    <button @click="dismiss" class="px-4 py-2 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-md hover:bg-gray-50 dark:bg-zinc-800 dark:text-zinc-200 dark:border-zinc-600 dark:hover:bg-zinc-700">
                        Close
                    </button>
                    <button @click="copyToClipboard" class="px-4 py-2 text-sm font-medium text-white bg-blue-600 rounded-md hover:bg-blue-700 dark:bg-blue-700 dark:hover:bg-blue-600">
                        {{ hasCopied ? 'Copied!' : 'Copy to Clipboard' }}
                    </button>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import DialogUtils from "../../js/DialogUtils";

export default {
    name: "PaperMessageDialog",
    data() {
        return {
            isShowing: false,
            uri: "",
            hasCopied: false,
        };
    },
    methods: {
        show(uri) {
            this.uri = uri;
            this.hasCopied = false;
            this.isShowing = true;
        },
        dismiss() {
            this.isShowing = false;
        },
        async copyToClipboard() {
            try {
                await navigator.clipboard.writeText(this.uri);
                this.hasCopied = true;
            } catch(e) {
                DialogUtils.alert("Failed to copy paper message to clipboard");
                console.log(e);
            }
        },
    },
}
</script>
