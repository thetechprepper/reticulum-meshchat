<template>
    <div class="flex flex-col flex-1 overflow-hidden min-w-full sm:min-w-[500px] dark:bg-zinc-950">
        <div class="overflow-y-auto space-y-2 p-2">

            <div class="bg-white dark:bg-zinc-800 rounded shadow">
                <div class="flex border-b border-gray-300 dark:border-zinc-700 text-gray-700 dark:text-gray-200 p-2 font-semibold">Import Paper Message</div>
                <div class="dark:divide-zinc-700 text-gray-900 dark:text-gray-100 p-2 space-y-2">

                    <div>
                        <button @click="pasteFromClipboard" type="button" class="inline-flex items-center rounded-md bg-blue-500 px-2.5 py-1.5 text-sm font-semibold text-white shadow-sm hover:bg-blue-400 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-500 dark:bg-blue-600 dark:hover:bg-blue-500 dark:focus-visible:outline-blue-600">
                            Paste from Clipboard
                        </button>
                    </div>

                    <textarea
                        v-model="paperMessageUri"
                        class="bg-gray-50 border border-gray-300 dark:border-zinc-800 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-zinc-800 dark:text-zinc-100 dark:border-zinc-900"
                        rows="8"
                        placeholder="lxm://"></textarea>

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
        };
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
    },
}
</script>
