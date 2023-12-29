<script setup lang="ts">
import { ref } from "vue";
import { invoke } from "@tauri-apps/api/tauri";
import { useRouter } from "vue-router";

const router = useRouter();
const info = ref("");
const error = ref("");

const fetchData = async () => {
    info.value = "登录中...";
    let sessionAlive: boolean = false;
    let callback: { status: boolean; is_alive: boolean; error: string };

    if (localStorage.getItem("session_key") != null && localStorage.getItem("server") != null) {
        callback = JSON.parse(
            await invoke("session_alive", { server: localStorage.getItem("server"), sessionkey: localStorage.getItem("session_key") })
        );
        if (callback.status) {
            sessionAlive = callback.is_alive;
        } else {
            error.value = callback["error"];
            await new Promise(resolve => setTimeout(resolve, 20000));
            sessionAlive = false;
        }
    } else {
        sessionAlive = false;
    };

    if (!sessionAlive) {
        error.value = "登录验证失败，请重新登陆！";
        localStorage.removeItem("session_key");
        localStorage.removeItem("isLoggedIn");
        await new Promise(resolve => setTimeout(resolve, 2000));
    }
    return sessionAlive;
};

fetchData().then((sessionAlive) => {
    if (!sessionAlive) {
        localStorage.removeItem("isLoggedIn");
        router.push({ path: "/login" });
    } else {
        localStorage.setItem("isLoggedIn", "true");
        router.push({ path: "/dashboard" });
    }
});
</script>

<template>
    <div class="card flex align-items-center justify-content-center" style="padding-top: 39vh;">
        <ProgressSpinner style="width: 17%; height: 17%" strokeWidth="4" animationDuration="1s" aria-label="预加载..." />
    </div>
    <div class="card flex align-items-center justify-content-center" style="padding-top: 20vh;">
        <small class="p-info" id="text-info">{{ info || null }}</small>
        <small class="p-error" id="text-error">{{ error || null }}</small>
    </div>
</template>

<style scoped></style>