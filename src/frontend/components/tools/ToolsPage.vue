<template>
    <div class="flex flex-col flex-1 overflow-hidden min-w-full sm:min-w-[500px] dark:bg-zinc-950">
        <div class="overflow-y-auto space-y-2 p-2">

            <!-- appearance -->
            <div class="bg-white dark:bg-zinc-800 rounded shadow">
                <div class="flex border-b border-gray-300 dark:border-zinc-700 text-gray-700 dark:text-gray-200 p-2 font-semibold">Tools</div>
                <div class="dark:divide-zinc-700 text-gray-900 dark:text-gray-100 p-2">
                    A collection of useful tools bundled with MeshChat
                </div>
            </div>

            <!-- ping -->
            <RouterLink :to="{ name: 'ping' }" class="group flex bg-white dark:bg-zinc-800 p-2 rounded shadow hover:bg-gray-50 dark:hover:bg-zinc-700">
                <div class="mr-2">
                    <div class="flex bg-gray-300 text-gray-500 rounded shadow p-2">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="size-10">
                            <path fill-rule="evenodd" d="M14.615 1.595a.75.75 0 0 1 .359.852L12.982 9.75h7.268a.75.75 0 0 1 .548 1.262l-10.5 11.25a.75.75 0 0 1-1.272-.71l1.992-7.302H3.75a.75.75 0 0 1-.548-1.262l10.5-11.25a.75.75 0 0 1 .913-.143Z" clip-rule="evenodd" />
                        </svg>
                    </div>
                </div>
                <div class="my-auto mr-auto dark:text-gray-200">
                    <div class="font-bold">Ping</div>
                    <div class="text-sm">Allows you to ping a destination hash.</div>
                </div>
                <div class="my-auto text-gray-400 group-hover:text-gray-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5"></path>
                    </svg>
                </div>
            </RouterLink>

            <!-- rnode flasher -->
            <a target="_blank" href="/rnode-flasher/index.html" class="group flex bg-white dark:bg-zinc-800 p-2 rounded shadow hover:bg-gray-50 dark:hover:bg-zinc-700">
                <div class="mr-2">
                    <div class="flex bg-gray-300 text-white rounded shadow">
                        <img src="/rnode-flasher/reticulum_logo_512.png" class="size-14"/>
                    </div>
                </div>
                <div class="my-auto mr-auto dark:text-gray-200">
                    <div class="font-bold">RNode Flasher</div>
                    <div class="text-sm">Flash RNode firmware to supported devices.</div>
                </div>
                <div class="my-auto text-gray-400 group-hover:text-gray-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5"></path>
                    </svg>
                </div>
            </a>

            <!-- Import paper message -->
            <RouterLink :to="{ name: 'paper-message-import' }" class="group flex bg-white dark:bg-zinc-800 p-2 rounded shadow hover:bg-gray-50 dark:hover:bg-zinc-700">
                <div class="mr-2">
                    <div class="flex bg-gray-300 text-gray-500 rounded shadow p-2">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-10">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 14.25v-2.625a3.375 3.375 0 0 0-3.375-3.375h-1.5A1.125 1.125 0 0 1 13.5 7.125v-1.5A3.375 3.375 0 0 0 10.125 2.25H8.25m0 12.75h7.5m-7.5 3h4.5m-1.5-15.75H5.625c-.621 0-1.125.504-1.125 1.125v17.25c0 .621.504 1.125 1.125 1.125h12.75c.621 0 1.125-.504 1.125-1.125V11.25a9 9 0 0 0-9-9Z" />
                        </svg>
                    </div>
                </div>
                <div class="my-auto mr-auto dark:text-gray-200">
                    <div class="font-bold">Import Paper Message</div>
                    <div class="text-sm">Import an LXMF paper message.</div>
                </div>
                <div class="my-auto text-gray-400 group-hover:text-gray-500">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m8.25 4.5 7.5 7.5-7.5 7.5"></path>
                    </svg>
                </div>
            </RouterLink>

        </div>
    </div>
</template>

<script>

export default {
    name: 'ToolsPage',
}
</script>
