<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
// import Detail from "./Detail.vue";
import Project from './Detail/Project.vue';

const menulist = ref([
    { id: "menu_project", title: 'Project', color: 'blue', checked: true },
    { id: "menu_todo", title: 'Todo', color: 'yellow' },
    { id: "menu_task", title: 'Task', color: 'red' }
])

const visible = ref(false);
const nickname = ref("N/A");
const favicon = ref("");

const fetchData = async () => {
    let staged_nickname = localStorage.getItem("nickname");
    if (staged_nickname != null) {
        nickname.value = staged_nickname;
    };

    let callback: { status: boolean; username: string; nickname: string; favicon: string; error: string };

    if (localStorage.getItem("session_key") != null && localStorage.getItem("server") != null) {
        callback = JSON.parse(
            await invoke("account_handler", { server: localStorage.getItem("server"), sessionkey: localStorage.getItem("session_key") })
        );

        if (callback.status) {
            return callback
        };
    };
    return null;
}

fetchData().then((callback) => {
    if (callback !== null) {
        nickname.value = callback.nickname;
        favicon.value = callback.favicon;
    }
});
</script>


<template>
    <div class="card">
        <Toolbar>
            <template #start>
                <Button icon="pi pi-bars" class="mr-2" @click="visible = true"></Button>
            </template>

            <template #center>
            </template>

            <template #end>
                <span class="p-input-icon-left">
                    <i class="pi pi-search"></i>
                    <InputText placeholder="Search" />
                </span>
            </template>
        </Toolbar>
    </div>
    <div class="card flex justify-content-center">
        <Sidebar v-model:visible="visible">
            <template #container="{ closeCallback }">
                <div class="flex flex-column h-full">
                    <div class="flex align-items-center justify-content-between px-4 pt-3 flex-shrink-0">
                        <span class="inline-flex align-items-center gap-2">
                            <!-- <svg width="35" height="40" viewBox="0 0 35 40" fill="none" xmlns="http://www.w3.org/2000/svg">
                                <path
                                    d="M25.87 18.05L23.16 17.45L25.27 20.46V29.78L32.49 23.76V13.53L29.18 14.73L25.87 18.04V18.05ZM25.27 35.49L29.18 31.58V27.67L25.27 30.98V35.49ZM20.16 17.14H20.03H20.17H20.16ZM30.1 5.19L34.89 4.81L33.08 12.33L24.1 15.67L30.08 5.2L30.1 5.19ZM5.72 14.74L2.41 13.54V23.77L9.63 29.79V20.47L11.74 17.46L9.03 18.06L5.72 14.75V14.74ZM9.63 30.98L5.72 27.67V31.58L9.63 35.49V30.98ZM4.8 5.2L10.78 15.67L1.81 12.33L0 4.81L4.79 5.19L4.8 5.2ZM24.37 21.05V34.59L22.56 37.29L20.46 39.4H14.44L12.34 37.29L10.53 34.59V21.05L12.42 18.23L17.45 26.8L22.48 18.23L24.37 21.05ZM22.85 0L22.57 0.69L17.45 13.08L12.33 0.69L12.05 0H22.85Z"
                                    fill="var(--primary-color)"
                                />
                                <path
                                    d="M30.69 4.21L24.37 4.81L22.57 0.69L22.86 0H26.48L30.69 4.21ZM23.75 5.67L22.66 3.08L18.05 14.24V17.14H19.7H20.03H20.16H20.2L24.1 15.7L30.11 5.19L23.75 5.67ZM4.21002 4.21L10.53 4.81L12.33 0.69L12.05 0H8.43002L4.22002 4.21H4.21002ZM21.9 17.4L20.6 18.2H14.3L13 17.4L12.4 18.2L12.42 18.23L17.45 26.8L22.48 18.23L22.5 18.2L21.9 17.4ZM4.79002 5.19L10.8 15.7L14.7 17.14H14.74H15.2H16.85V14.24L12.24 3.09L11.15 5.68L4.79002 5.2V5.19Z"
                                    fill="var(--text-color)"
                                />
                            </svg> -->
                            <span class="font-semibold text-2xl text-primary">Quantumix</span>
                        </span>
                        <span>
                            <Button type="button" @click="closeCallback" icon="pi pi-times" rounded outlined
                                class="h-2rem w-2rem"></Button>
                        </span>
                    </div>
                    <div class="overflow-y-auto">
                        <ul class="list-none p-3 m-0">
                            <li>
                                <ul class="list-none p-0 m-0 overflow-hidden">
                                    <li>
                                        <a v-ripple
                                            class="flex align-items-center cursor-pointer p-3 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                                            <i class="pi pi-home mr-2"></i>
                                            <span class="font-medium">主页</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a v-ripple
                                            class="flex align-items-center cursor-pointer p-3 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                                            <i class="pi pi-bookmark mr-2"></i>
                                            <span class="font-medium">书签</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a v-ripple
                                            class="flex align-items-center cursor-pointer p-3 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                                            <i class="pi pi-comments mr-2"></i>
                                            <span class="font-medium">消息</span>
                                            <span
                                                class="inline-flex align-items-center justify-content-center ml-auto bg-primary border-circle"
                                                style="min-width: 1.5rem; height: 1.5rem">0</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a v-ripple
                                            class="flex align-items-center cursor-pointer p-3 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                                            <i class="pi pi-calendar mr-2"></i>
                                            <span class="font-medium">日历</span>
                                        </a>
                                    </li>
                                    <li>
                                        <a v-ripple
                                            class="flex align-items-center cursor-pointer p-3 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                                            <i class="pi pi-cog mr-2"></i>
                                            <span class="font-medium">设置</span>
                                        </a>
                                    </li>
                                </ul>
                            </li>
                        </ul>
                    </div>
                    <div class="mt-auto">
                        <hr class="mb-3 mx-3 border-top-1 border-none surface-border" />
                        <a v-ripple
                            class="m-3 flex align-items-center cursor-pointer p-3 gap-2 border-round text-700 hover:surface-100 transition-duration-150 transition-colors p-ripple">
                            <Avatar image="{{ favicon }}" shape="circle" />
                            <span class="font-bold">{{ nickname }}</span>
                        </a>
                    </div>
                </div>
            </template>
        </Sidebar>
    </div>

    <main>
        <Project :title="menulist[0].title" :color="menulist[0].color" :display="menulist[0].checked"></Project>
    </main>
</template>

<style scoped>
main {
    height: 100%;
    position: static;
    padding-bottom: 6%;
}
</style>
