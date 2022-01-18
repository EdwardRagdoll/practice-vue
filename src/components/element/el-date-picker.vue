<template>
    <div class="block">
      <el-date-picker
        v-model="value2"
        align="right"
        type="date"
        placeholder="选择日期"
        :picker-options="pickerOptions"
      >
      </el-date-picker>
    </div>
</template>

<script>
export default {
  name: "date-picker",
  data() {
    return {
      pickerOptions: {
        disabledDate(time) {
        //   return time.getTime() > Date.now();    // 今天及今天以前的日期
          return time.getTime() <= Date.now()     // 今天及今天以前的日期
         // time < Date.now() - 24 * 60 * 60 * 1000   // 今天及今天以前的日期
        },
        shortcuts: [
          {
            text: "今天",
            onClick(picker) {
              picker.$emit("pick", new Date());
            },
          },
          {
            text: "昨天",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit("pick", date);
            },
          },
          {
            text: "一周前",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", date);
            },
          },
        ],
      },
      value1: "",
      value2: "",
    };
  },
  methods: {
    disabledDate(date) {
      return date < Date.now() - 24 * 60 * 60 * 1000;
    },
  }
};
</script>