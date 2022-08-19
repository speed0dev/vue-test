<template>
    <div>
        <h1>UserInfo</h1>
        <div>사용자 정보</div>
        <div>
            <table :style="{color: props.color}">
                <tr>
                    <td>이름:</td>
                    <td>
                        <input ref="txt_nm"
                            v-model="info_val.user_nm"
                            placeholder="이름을 입력하세요."
                        >
                    </td>
                </tr>
                <tr>
                    <td>나이:</td>
                    <td>
                        <input type="number" v-model="info_val.user_age" />
                    </td>
                </tr>

                <tr>
                    <td>지역:</td>
                    <td>
                        <select v-model="info_val.user_local">
                            <option
                                v-for="(option, idx) in props.locals"
                                v-bind:value="option.value"
                                :key="idx"
                            >{{option.name}}
                            </option>
                        </select>
                    </td>
                </tr>

                <tr>
                    <td>취미:</td>
                    <td>
                        <input type="checkbox" value="s" v-model="info_val.user_hobby" />축구
                        <input type="checkbox" value="b" v-model="info_val.user_hobby" />농구
                        <input type="checkbox" value="a" v-model="info_val.user_hobby" />야구
                    </td>
                </tr>

                <tr :style="{display:props.usehobby == true? '':'none'}">
                    <td style="text-align: end" colspan="2" @click="onConfirmClick">
                        <button>확인</button>
                    </td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>

import {
    ref, reactive, onMounted, onUpdated
} from 'vue';

export default {
    components: {},
    name: 'user-info',
    
    //
    props: {
        color: {
            type: String,
            default: 'blue'
        },
        usehobby: {
            type: Boolean,
            default: true
        },
        locals:{
            type: Array,
            default: [
                {name: "서울", value: "1"},
                {name: "부산", value: "2"},
                {name: "인천", value: "3"},
            ]
        }
    },

    emits:['comfirm'],

    // context ? 
    setup(props, context) {
        const txt_nm = ref(null);

        const info_val = reactive({
            user_nm: "",
            user_age: 20,
            user_local: "1",
            user_hobby: ['s', 'b']
        });

        //
       
        const onConfirmClick = () => {
            //console.log(context);
            //
            context.emit('comfirm', info_val);
        };

        onMounted(()=>{
            console.log("[UserInfo]onMounted!");
            txt_nm.value.focus();

        });

        onUpdated(() => {
            console.log("[UserInfo]onUpdated!");

        });
        
        return {
            onConfirmClick,
            props,
            info_val,
            txt_nm
        }
    },
}
</script>