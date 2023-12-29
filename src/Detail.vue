<script setup lang="ts">
import { ref } from 'vue';
import Task from './components/Detail/Task.vue';
import Todo from './components/Detail/Todo.vue';
import Project from './components/Detail/Project.vue';

const title = "Quantumix";
const menulist = ref([
    { id: "menu_project", title: 'Project', color: 'blue', checked: true },
    { id: "menu_todo", title: 'Todo', color: 'yellow' },
    { id: "menu_task", title: 'Task', color: 'red' }
])

function clickMenu(e: any) {
    menulist.value.forEach(
        menu => menu.id === e.target.id ? menu.checked = true : menu.checked = false
    )
}

function clickMenuOpen() {
    let ele = document.getElementById("menuDiv");
    if (ele != null) {
        ele.classList.toggle("closed");
    }
}
</script>

<template>
    <menu id="menuDiv">
        <img alt="Quantumix logo" class="logo" src="@/assets/logo.svg" />
        <h1>{{ title }}</h1>
        <ul>
            <li @click="clickMenu" class="menuButton" :color="menu.color" v-for="menu in menulist" :id="menu.id"
                :checked="menu.checked">{{ menu.title }}</li>
        </ul>
    </menu>
    <main>
        <div class="topbar">
            <button id="menuOpen" @click="clickMenuOpen"></button>
        </div>
        <Project :title="menulist[0].title" :color="menulist[0].color" :display="menulist[0].checked"></Project>
        <Todo :title="menulist[1].title" :color="menulist[1].color" :display="menulist[1].checked"></Todo>
        <Task :title="menulist[2].title" :color="menulist[2].color" :display="menulist[2].checked"></Task>
    </main>
</template>

<style scoped>
/* ————————————————目录———————————————— */
@media (min-width: 1024px) {

    /* 宽屏 */
    menu {
        height: 100%;
        padding-top: 100px;
        width: 280px;
        z-index: 1;
        float: left;
    }

    menu h1 {
        font-size: 2.6rem;
        position: relative;
        line-height: 2em;
        margin-bottom: 20px;
    }

    menu .logo {
        width: 80px;
        height: 80px;
        padding: 10px;
        display: block;
        margin: 0 auto;
    }

    menu.closed {
        margin-left: -300px;
        margin-top: 0;
    }

    menu ul {
        flex-direction: column;
    }

    menu ul li {
        margin-top: 10px;
    }

    menu .menuButton {
        font-size: 1.5rem;
        padding: 5px;
    }
}

@media (max-width: 1024px) {

    /* 窄屏 */

    menu .logo,
    menu h1 {
        display: none;
    }

    menu ul {
        /* 顶部栏高度 */
        margin-top: 60px;
        flex-direction: row;
        height: 40px;
        line-height: 40px;
    }

    menu li {
        flex-grow: 1;
    }

    menu.closed ul {
        height: 0;
        overflow: hidden;
    }
}

menu {
    transition: all 0.3s;
}

menu h1 {
    font-weight: bolder;
    text-align: center;
}

menu ul {
    display: flex;
    transition: all 0.3s;
}

menu ul li {
    list-style: none;
}

menu .menuButton {
    text-align: center;
    font-weight: bolder;
}

/* ————————————————主内容———————————————— */
main {
    height: 100%;
    position: static;
}

/* ————————头部栏———————— */
.topbar {
    width: 100%;
}

#menuOpen {
    width: 60px;
    height: 60px;
    /* position: absolute; */
    z-index: 2;
    left: 0;
    top: 0;
    border: none;
}

#menuOpen::before {
    font-size: 1.5em;
    content: "三";
}

@media (min-width: 1024px) {

    /* 宽屏 */
    .topbar {
        height: 60px;
    }
}

@media (max-width: 1024px) {

    /* 窄屏 */
    .topbar {
        height: 60px;
        position: absolute;
        top: 0;
    }
}
</style>
