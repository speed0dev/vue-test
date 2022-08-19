<template>
    <div class="content">
        <div>My Page</div>

        <div>
            <h1>Test</h1>
            <div>{{info}}</div>
            <div>
                <button @click="onBtnClick">{{btnCap}}</button><br/>
                <button @click="onBtnClick2">{{info2}}</button>
            </div>
        </div>

        <div>
            <div>데이터1: <input type="text" v-model="txt_val" />{{txt_val}}</div>
            <div>데이터2: <input type="text" v-model="txt_val2" />{{txt_val2}}</div>
        </div>

        <div>

            <input type="checkbox" v-model="chk_vals.soccer" />축구
            <input type="checkbox" v-model="chk_vals.basketball" />농구
            <span :style="{color: chk_vals.result[1]==1? 'red':'blue'}">{{chk_vals.result[0]}}</span>
        </div>

        <div>
            <h1>Radio</h1>
            <div> 
                <input type="radio" value="java" v-model="rdo_val" />Java
                <input type="radio" value="C" v-model="rdo_val" />C 
                <input type="radio" value="Python" v-model="rdo_val" />Python
                <span>선택된 값:{{rdo_val}} </span>
            </div>
            <div>
                <input type="radio" value="1" name="rd1" />AA
                <input type="radio" value="2" name="rd1" />BB
                <input type="radio" value="3" name="rd1" />CC
            </div>
            <div>
                <input type="radio" value="1" id="rd1" />AA_1
                <input type="radio" value="2" id="rd1" />BB_2
                <input type="radio" value="3" id="rd1" />CC_3
            </div>
        </div>

        <div>
            <h1>Select</h1>
            <select v-model="sel_val">
                <option
                    v-for="(option, idx) in options"
                    v-bind:value="option.value"
                    :key="idx"
                >
                {{option.text}}
                </option>
            </select>
            <br/>
            <span>선택값:{{ sel_val }}</span>
        </div>

    </div>
</template>


<script>
import{
    computed,       //
    reactive,       //
    ref,            //
} from 'vue';



const g_Codes = "";


export default {

    name: 'Button',
    components: {},
    setup() {

        const info = "정보입니다.";

        const btnCap = "선택확인";

        const info2 = ref("기본값입니다. info2");   //


        //const num = 1;

        const txt_val = "checkName";

        const txt_val2 = ref("기본값");

        let number  = 1;
        const onBtnClick = ()=> {
            console.log("[click]");
            info = "변경된 정보입니다.";
        };

        const onBtnClick2 = () => {
            info2.value = "변경되어진 정보" + number;
            ++number;
            
        }

        // checkBox
        // reactive 
        const chk_vals = reactive({
            soccer: true,
            basketball: false,

            //
            result: computed(()=>{
                const hobbys = [];

                if(chk_vals.soccer){
                    hobbys.push('축구');
                }

                if(chk_vals.basketball){
                    hobbys.push('농구');
                }

                return hobbys.length == 0
                    ? ['취미를 선택하세요.', 1]
                    : ['선택하신 취미는: ' + hobbys.join(",") + '입니다.', 2]
            }),

        });

        // 
        const rdo_val = ref("Java");

        const sel_val = ref("1");     // 숫자?

        const options = [
            {text:'서울', value:"1"}      //
            ,{text:'부산', value:"2"}     //
            ,{text:'인천', value:"3"}     //
        ]


        return {
            info,
            btnCap,

            // event
            onBtnClick,

            info2,
            onBtnClick2,

            txt_val,

            txt_val2,

            chk_vals,

            rdo_val,

            sel_val,
            options,
        };
        
    }

    
}
</script>


<style>
.content{

}

</style>