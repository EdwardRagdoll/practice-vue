<template>
    <div>
        我是儿子：
        <el-button @click="test">打印祖父的年龄</el-button>
    </div>
</template>

<script>
export default {
    name: "Son",
    data() {
        return {

        }
    },
    methods: {
        test() {
            console.log(this.$attrs.age);
            this.$emit("printGrandPaAge")
        }
    }    
}
</script>