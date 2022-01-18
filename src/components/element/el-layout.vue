<template>
  <el-container>
    <el-header>
      <el-select v-model="selected" placeholder="请选择">
        <el-option
          v-for="item in layouts"
          :key="item.value"
          :label="item.name"
          :value="item.value">
        </el-option>
      </el-select>
    </el-header>
    <el-main>
      <div class="block" style="width: 1200px;height:400px">

        <!--  1*1 布局 -->
        <div style="height:100%;width:100%" v-if="selected==0">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="24"><div class="grid-content"></div></el-col>
          </el-row>
        </div>

        <!-- 2*1 布局 -->
        <div style="height:100%;width:100%" v-else-if="selected==1">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
        </div>

        <!-- 2*2 布局 -->
        <div style="height:100%;width:100%" v-else-if="selected==2">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
        </div>

        <!-- 3*2 布局 -->
        <div style="height:100%;width:100%" v-else-if="selected==3">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="12"><div class="grid-content"></div></el-col>
            <el-col :span="12"><div class="grid-content"></div></el-col>
          </el-row>
        </div>

        <!-- 3*3 布局 -->
        <div style="height:100%;width:100%" v-else-if="selected==4">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
          </el-row>
        </div>

        <!-- 1+5 布局 -->
        <div style="height:100%;width:100%" v-else-if="selected==5">
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
            <el-col :span="8"><div class="grid-content"></div></el-col>
          </el-row>
          <el-row :gutter="20" type="flex" justify="center">
            <el-col :span="8">
              <el-row><div class="grid-content"></div></el-row>
              <el-row><div class="grid-content"></div></el-row>
            </el-col>
            <el-col :span="16">
              <div class="big-content"></div>
            </el-col>
          </el-row>
        </div>
      </div>
    </el-main>
  </el-container>
</template>

<script>
export default {
  name: 'Layout',
  data() {
    return {
      selected: 0,
      layouts: [
        { 'name': '1x1模式', 'value': 0 },
        { 'name': '2x1模式', 'value': 1 },
        { 'name': '2x2模式', 'value': 2 },
        { 'name': '3x2模式', 'value': 3 },
        { 'name': '3x3模式', 'value': 4 },
        { 'name': '1+5模式', 'value': 5 }
      ],
    };
  },
};
</script>

<style scoped>
.el-row {
  min-height: 100px;
  /* background-color: aqua; */
  margin-bottom: 20px;
}

.el-col {
  
  border-radius: 5px;
}

.grid-content {
  width: 100%;
  height: 100%;
  min-height: 100px;
  background-color: brown;
  border-radius: 5px;
}

.big-content {
  width: 100%;
  height: 220px;
   background-color: brown;
   border-radius: 5px;
}
</style>