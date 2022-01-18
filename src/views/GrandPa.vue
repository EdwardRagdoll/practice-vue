<template>
    <div>
        我是祖父: 下面是爸爸
        <Parent :gender="gender" :age="age" @printGrandPaAge="printGrandPaAge" />
        <el-button @click="age++">增加祖父年龄</el-button>
    </div>
</template>

<script>
import Parent from "./Parent.vue"
export default {
    name: "GrandPa",
    components: {
        Parent
    },
    data() {
        return {
            age: 65,
            gender: "男"
        }
    },
    methods: {
        printGrandPaAge() {
            console.log(this.age);
        }
    }    
}
</script>

