<template>
    <div>
        我是爸爸： 下面是儿子
        <Son v-bind="$attrs" v-on="$listeners" />
    </div>
</template>

<script>
import Son from "./Son.vue"
export default {
    name: "Parent",
    components: {
        Son
    },
    data() {
        return {
            
        }
    },   
}
</script>

