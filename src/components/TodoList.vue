<template>
    <div></div>
    <h1>Todo List</h1>
    <div>
        <div>
            <input ref="ref_title"
                placeholder="할 일을 입력하세요."
                v-model="txt_title"
            />
            <button style="margin-left:10px; width:100px; height:32px;"
                @click="onAddClick"
            >추가</button>
        </div>
        <div style="">
            <ol>
                <li v-for="(data, idx) in todoList" :key="idx">    
                    <div>{{data}} <button @click="onDelClick(idx)">삭제</button></div>
                </li>
            </ol>
        </div>
    </div>
</template>

<script>
import { 
    ref,
    reactive,
 } from 'vue'

// export default ?
export default {
    components:{},
    name: "todo-list",
    props: {},
    emits: ['comfirm'],

// https://hianna.tistory.com/489
// javascript 배열 삭제
    setup() {
        const ref_title = ref(null);
        const todoList = reactive(['Java', 'C']);
        const txt_title = ref(" ");

        const onAddClick = () => {
            if(txt_title.value === ""){
                alert("입력하세요!");
                ref_title.value.focus();
                return;
            }
            todoList.push(txt_title.value);
            txt_title.value = '';
            ref_title.value.focus();

        };

        const onDelClick = (idx) => {
            if(window.confirm("삭제 합니까?")){
                todoList.splice(idx, 1);
            }
            return;
        };



        return {
            todoList, txt_title, ref_title, onAddClick, onDelClick,    
        }
        
    },
}
</script>
