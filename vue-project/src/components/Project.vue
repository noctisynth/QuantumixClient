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
const projectList = [
    {
        "title": "项目标题",
        "content": ["项目的一些描述介绍简介什么的，项目的一些描述介绍简介什么的，项目的一些描述介绍简介什么的，项目的一些描述介绍简介什么的，项目的一些描述介绍简介什么的，项目的一些描述介绍简介什么的。",
            "第二段文字第二段文字第二段文字第二段文字第二段文字第二段文字第二段文字"],
        "projectId": "project123",
        "todo": [
            {
                "Table": "Todo",
                "Id": "todo123",
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
                "Table": "Todo",
                "Id": "todo123",
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
                "Table": "Todo",
                "Id": "todo123",
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
                "Table": "Todo",
                "Id": "todo123",
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
        ],
        "task": [
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
        ]
    }
]
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

function getUserImage(uid) {
    // 获取用户头像
    return "src/components/userImage/" + uid + ".jpg";
}
function getUserName(uid) {
    // 获取用户昵称
    return "用户" + uid;
}

</script>


<template>
    <div class="mainContent" :class="title" :color="color">
        <h2>{{ title }}</h2>
        <div class="project" v-for="p in projectList" :id="projectId">
            <h3>{{ p.title }}</h3>
            <p v-for="content in p.content">{{ content }}</p>
            <div class="projectDark">
                <h3>Todo</h3>
                <div class="todo" v-for="todo in p.todo" :id="todo.Id">
                    <div class="listmain" @click="clickListmain">
                        <div class="listmainCont">
                            <div class="title">{{ todo.Name }}</div>
                            <div class="cont">{{ todo.Content }}</div>
                        </div>
                        <div class="listmainCont">
                            <div class="title">开始时间</div>
                            <div class="cont">{{ todo.StartLine }}</div>
                        </div>
                        <div class="listmainCont">
                            <div class="title">结束时间</div>
                            <div class="cont">{{ todo.EndLine }}</div>
                        </div>
                        <div class="listmainCont userImage">
                            <img :src="getUserImage(todo.UserID)" alt="用户头像">
                            <div class="title">用户</div>
                            <div class="cont">{{ getUserName(todo.UserID) }}</div>
                        </div>
                    </div>
                    <div class="listmore">
                        <div class="listmoreCont">
                            <div class="title">介绍</div>
                            <div class="cont">{{ todo.Description }}</div>
                        </div>
                        <div class="listmoreCont">
                            <div class="title">ID</div>
                            <div class="cont">{{ todo.Id }}</div>
                        </div>
                    </div>
                </div>
                <h3>Task</h3>
                <div class="task" v-for="task in p.task" :id="task.Id">
                    <div class="listmain" @click="clickListmain">
                        <div class="listmainCont">
                            <div class="title">{{ task.Name }}</div>
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

/* ————————todo———————— */
.todo,
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

/* 用户头像 */
.userImage img {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    border: 2px solid;
    display: block;
    float: left;
    margin-right: 10px;
}

/* project */
.project {
    margin: 10px 0;
    border-radius: 10px;
    overflow: hidden;
}

.project h3 {
    padding: 10px;
}

.project p {
    padding: 5px 10px;
}

.projectDark {
    padding: 5px 15px;
    margin-top: 10px;
}

.projectDark .task,
.projectDark .todo {
    margin-left: 40px;
}


.projectDark .task::before,
.projectDark .todo::before {
    content: "";
    width: 5px;
    height: 5px;
    position: absolute;
    left: -23px;
    top: 24px;
    border-radius: 5px;
    border: 1px solid;
}

.projectDark .task::after,
.projectDark .todo::after {
    content: "";
    height: calc(100% + 5px);
    border-left: 1px dashed;
    opacity: 0.5;
    width: 5px;
    position: absolute;
    left: -20px;
    top: 0;
}

.projectDark .task:nth-last-child(1)::after {
    height: 24px;
}
</style>