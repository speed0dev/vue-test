<template>
    <div>MyApp</div>
    <div>{{appName}}</div>

    <hr />
    <div><todo-list /></div>
    <div><user-info :color="color" :usehobby="hobby" @comfirm="onConfirmClick" /></div>


</template>


<script>
import { ref } from 'vue';
import TodoList from '../../components/TodoList.vue' ;
import UserInfo from '../../components/UserInfo.vue';

export default {
    name: 'MyApp',
    components: { TodoList, UserInfo},

    setup() {
        
        const colors = [
            {name: "빨강", value:"red"}
            ,{name: "파랑", value:"blue"}
            ,{name: "노강", value:"yellow"}
        ]

        const color = ref('red');

        const appName = "appName";

        const hobby = ref(true);

        //
        const onConfirmClick = (d) =>{
            console.log(d);

        };

        return{

            appName,

            hobby,
            onConfirmClick,
        }

    },
}
</script>