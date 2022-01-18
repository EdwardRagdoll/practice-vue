<template>
  <anji-crud ref="listPage" :option="crudOption" @handleCustomValue="handleCustomValue">

    <!-- table操作列按钮插槽 -->
    <template v-slot:edit="row">
        <el-button type="text" @click="handleDetailOperation(row)">新操作</el-button>
    </template>

    <!-- 自定义表格内容，覆盖下方option设置内容 -->
    <!-- <template v-slot:tableColumn="tableData">
      <el-table-column prop="field" label="label">

      </el-table-column>
    </template> -->

    <!-- table操作列插入按钮 -->
    <template v-slot:rowButton="row">
        <el-button @click="handleRow(row)">新的行操作</el-button>
    </template>

    <!-- 编辑弹窗插入表单 -->
    <!-- <template v-slot:cardInEditPage="rowData">

    </template> -->

    <!-- 编辑弹窗下方插入按钮 -->
    <!-- <template v-slot:editBtnPage="rowData">

    </template> -->

    <!-- 底部插入html -->
    <template v-slot:pageSection>
        <div>插入底部html片段</div>
    </template>

    <!-- table做上架插入批量操作按钮 -->
    <template v-slot:buttonLeftOnTable> </template>

    <!--
        <template slot="rowButton" slot-scope="props">
            <el-button type="primary" @click="customButtom(props)">行按钮</el-button>
        </template>
        -->
    <!--自定义的卡片插槽，将在编辑详情页面，出现在底部新卡片-->
    <!--这里可以将自定义的弹出框代码，放入到page中
        <template v-slot:pageSection>
          <div>插入底部html片段</div>
        </template>
        -->
  </anji-crud>
</template>
<script>
  import {
    queryListApi,
    queryDetailApi,
    addApi,
    deleteBatchApi,
    updateApi
  } from "@/api/accessAuthority";
  export default {
    name: "AccessAuthority",
    data() {
      return {
        crudOption: {
          useDefaultEdit:true,  // 是否使用CRUD内部编辑弹窗
          title: "权限管理",    // 弹框标题
          labelWidth: "120px", // 编辑弹窗表单中输入框左边的label文字宽度

          // 查询表单条件，包括左侧树，table上方的行内表单
          queryFormFields: [
            {
              inputType: "anji-tree", // 该类型将内容区一分为二，左侧20%显示树
              anjiTreeOption: {
                url: "/accessAuthority/menuTree", // 请求接口，将响应中id字段做为tree的id，将label字段做为tree的label
                enableFilter: true, // tree 是否有input 过滤
                isOpen: true // true tree 展开 false 关闭
              },
              label: "所属菜单", // 树顶部label文字
              field: "field1"   // 数查询选定节点后赋值的字段名
            },
            {
              inputType: "anji-select", //form表单类型 input|input-number|anji-select(传递url或者dictCode)|anji-tree(左侧树)|date|datetime|datetimerange
              anjiSelectOption: {
                dictCode: "ENABLE_FLAG",
                // ur: "/accessAuthority/menuTree"
              },
              label: "启用状态",
              field: "field2"
            },
            {
              inputType: "input",
              label: "菜单代码",
              field: "field2"
            },
          ],
          // 操作按钮
          buttons: {
            query: {    // 查询
              api: queryListApi,    // 分页列表请求方法， 默认pageSize-10，pageIndex-1
              permission: "authorityManage:query"   // 权限值
            },
            queryByPrimarykey: {    // 查询详情，打开编辑弹窗
              api: queryDetailApi,  // 详情查询方法，通常加accesskey
              permission: "authorityManage:query"
            },
            add: {      // 新增
              api: addApi,      // 新增数据API
              permission: "authorityManage:insert",
              isShow: true  // 控制新增按钮显隐
            },
            delete: {   // 批量删除，传参为数组
              api: deleteBatchApi,
              permission: "authorityManage:delete",
              isShow: true  // 控制删除按钮显隐
            },
            edit: {
              api: updateApi,   // 编辑完成提交调用API
              permission: "authorityManage:update"
            },
            customButton: {
              operationWidth: 150   // table操作列宽度
            }
          },
          // 表格列
          columns: [
            {
              label: "",
              field: "id",
              primaryKey: true, // 设定table主键列，编辑与查看详情时的参数
              tableHide: true,  // 表格中不显示
              editHide: true    // 编辑弹框中不显示
            },
            {
              label: "表头列文字", // 表头文字
              placeholder: "",  // 编辑弹窗中的控件默认提示文字
              field: "target",  // table列绑定字段名
              editField: "target",  // 编辑弹窗控件绑定字段名
              sortable: true,   // 是否可表头排序
              inputType: "input",   // 编辑弹窗内的控件类型，input|switch|input-number|anji-input|anji-select|date|checkbox|anji-cascader|anji-upload|anji-autocomplete|textarea
              rules: [  // 控件的表单校验规则
                { required: true, message: "目标菜单必填", trigger: "blur" },
                { min: 1, max: 64, message: "不超过64个字符", trigger: "blur" }
              ],
              disabled: false,   // 编辑弹窗中的空间是否禁止交互
              fieldTableRowRenderer: row => {   // 自定义表格列展示文字内容
                return `${row["targetName"]}[${row["target"]}]`;
              },
              renderer: (row) => {  // 表格里需要插入自定义html代码时使用,columnType设置为html
                return `<span style="display:inline-block;width:100px;height:30px;background:${row.color}"></span>`
              },
              columnType: "expand", // 控制表格列类型，默认不设置，expan|imgPreview|html|template
              minWidth: 110,     // 列最小宽度
              showOverflowTooltip: true,    // 是否展示tooltip
              columnComponent: null,    // columnType=template时使用
              mergeColumn: 'mergeField',    // 合并列字段
              colorStyle: {     // 控制文字样式，仅inputType为anji-crud内置拓展控件时有效
                0: "table-danger", //key为editField渲染的值（字典的提交值）'红色': 'danger','蓝色': 'primary','绿色': 'success','黄色': 'warning','灰色': 'info','白色'：''
                1: "table-success"
              },
            },
          ]
        }
      };
    },

    created() {},
    methods: {
        handleCustomValue(obj) {   // CRUD向外暴露方法，获取弹窗模式（查看/编辑）和行数据
            console.log(obj.type);
            console.log(obj.value);
        },
        handleDetailOperation(row) {

        },
        handleRow(row) {

        }
    }
  };
</script>
