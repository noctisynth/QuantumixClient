<script setup>
defineProps({
    title: {
        type: String,
        required: true
    },
    color: {
        type: String,
        required: true
    }
});
// 调用后端接口加载任务列表
const taskList = [
    {
        "Table": "Task",
        "Id": "task123",
        "ProjectID": 12345,
        "UserID": "user1",
        "Name": "测试任务",
        "Permission": "Public",
        "Priority": "Low",
        "Content": "这是一个测试任务",
        "Description": "这是一个测试任务",
        "StartLine": "2022-01-01T00:00:00",
        "EndLine": "2022-01-31T00:00:00",
        "Parent": 0,
        "IsChecked": false,
        "CreatedAt": "2022-01-01T00:00:00",
        "UpdatedAt": "2022-01-01T00:00:00"
    },
    {
        "Table": "Task",
        "Id": "task123",
        "ProjectID": 12345,
        "UserID": "user2",
        "Name": "测试任务测试任务测试任务",
        "Permission": "Public",
        "Priority": "Low",
        "Content": "这是一个测试任务",
        "Description": "这是一个测试任务",
        "StartLine": "2022-01-01T00:00:00",
        "EndLine": "2022-01-31T00:00:00",
        "Parent": 0,
        "IsChecked": false,
        "CreatedAt": "2022-01-01T00:00:00",
        "UpdatedAt": "2022-01-01T00:00:00"
    },
    {
        "Table": "Task",
        "Id": "task123",
        "ProjectID": 12345,
        "UserID": "user1",
        "Name": "测试任务",
        "Permission": "Public",
        "Priority": "Low",
        "Content": "这是一个测试任务",
        "Description": "这是一个测试任务",
        "StartLine": "2022-01-01T00:00:00",
        "EndLine": "2022-01-31T00:00:00",
        "Parent": 0,
        "IsChecked": false,
        "CreatedAt": "2022-01-01T00:00:00",
        "UpdatedAt": "2022-01-01T00:00:00"
    },
    {
        "Table": "Task",
        "Id": "task123",
        "ProjectID": 12345,
        "UserID": "user2",
        "Name": "测试任务测试任务测试任务",
        "Permission": "Public",
        "Priority": "Low",
        "Content": "这是一个测试任务",
        "Description": "这是一个测试任务",
        "StartLine": "2022-01-01T00:00:00",
        "EndLine": "2022-01-31T00:00:00",
        "Parent": 0,
        "IsChecked": false,
        "CreatedAt": "2022-01-01T00:00:00",
        "UpdatedAt": "2022-01-01T00:00:00"
    }
];
function clickListmain(e) {
    // 展开元素
    var div;
    if (e.target.tagName === 'DIV' && e.target.classList.contains('listmain')) {
        div = e.target;
    } else if (e.target.parentNode.classList.contains('listmain')) {
        div = e.target.parentNode;
    } else if (e.target.parentNode.parentNode.classList.contains('listmain')) {
        div = e.target.parentNode.parentNode;
    }
    div.parentNode.classList.toggle('expand');
}

function taskAccept(e) {
    console.log("接受任务");
    // 获取任务id
    var taskId = e.target.parentNode.parentNode.parentNode.id;
    // // 发送请求
    // var xhr = new XMLHttpRequest();
    // xhr.open("POST", "/api/task/accept", true);
    // xhr.setRequestHeader("Content-Type", "application/json");
    // xhr.onreadystatechange = function () {
    //     if (xhr.readyState === 4 && xhr.status === 200) {
    //         var response = JSON.parse(xhr.responseText);
    //         if (response.code === 200) {
    //             console.log("任务接受成功");
    //         } else {
    //             console.log("任务接受失败");
    //         }
    //     }
    // };
    // xhr.send(JSON.stringify({ taskId: taskId }));
}
function taskAbort(e) {
    console.log("放弃任务");
    // 获取任务id
    var taskId = e.target.parentNode.parentNode.parentNode.id;
    // // 发送请求
    // var xhr = new XMLHttpRequest();
    // xhr.open("POST", "/api/task/abort", true);
    // xhr.setRequestHeader("Content-Type", "application/json");
    // xhr.onreadystatechange = function () {
    //     if (xhr.readyState === 4 && xhr.status === 200) {
    //         var response = JSON.parse(xhr.responseText);
    //         if (response.code === 200) {
    //             console.log("任务放弃成功");
    //         } else {
    //             console.log("任务放弃失败");
    //         }
    //     }
    // };
    // xhr.send(JSON.stringify({ taskId: taskId }));
}
</script>


<template>
    <div class="mainContent" :class="title" :color="color">
        <h2>{{ title }}</h2>
        <div class="task" v-for="task in taskList" :id="task.Id">
            <div class="listmain" @click="clickListmain">
                <div class="listmainCont">
                    <div class="title">{{task.Name}}</div>
                    <div class="cont">{{ task.Content }}</div>
                </div>
                <div class="listmainCont">
                    <div class="title">开始时间</div>
                    <div class="cont">{{ task.StartLine }}</div>
                </div>
                <div class="listmainCont">
                    <div class="title">结束时间</div>
                    <div class="cont">{{ task.EndLine }}</div>
                </div>
            </div>
            <div class="listmore">
                <div class="listmoreCont">
                    <div class="title">介绍</div>
                    <div class="cont">{{ task.Description }}</div>
                </div>
                <div class="listmoreCont">
                    <div class="title">ID</div>
                    <div class="cont">{{ task.Id }}</div>
                </div>
                <div class="listmoreButton">
                    <button class="taskAccept" @click="taskAccept">接受</button>
                    <button class="taskAbort" @click="taskAbort">放弃</button>
                </div>
            </div>
        </div>
    </div>
</template>



<style scoped>
/* ————————信息内容———————— */
.mainContent {
    padding: 0 40px;
    max-width: 1680px;
    margin: 0 auto;
    height: calc(100% - 60px);
    overflow-y: scroll;
}

.mainContent h2 {
    font-size: 2rem;
    font-weight: bolder;
}

/* ————————task———————— */
.task {
    margin: 10px 0;
}

.listmain {
    border-radius: 10px;
    padding: 10px;
    display: flex;
}

.listmainCont {
    width: 220px;
    margin: 0 5px;
}

.listmainCont .title,
.listmoreCont .title {
    font-weight: bolder;
}

.listmore {
    border-radius: 0 0 10px 10px;
    /* padding: 10px 15px; */
    margin: 0 10px;
}

.listmoreCont {
    padding: 5px 0;
    padding: 5px 15px;
}

.listmore {
    position: relative;
    height: 0;
    overflow: hidden;
}

.expand .listmore {
    height: auto;
}

.listmoreButton {
    position: absolute;
    right: 0;
    bottom: 0;
    width: 80px;
}

.listmoreButton button {
    width: 100%;
    display: block;
    float: right;
    margin-bottom: 10px;
    padding: 5px 0;
}
</style>