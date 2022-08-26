<template>
  <div>
    <div
      style="
        background: #c0c0c0;
        width: 100%;
        padding: 40px;
        vertical-align: middle;
        text-align: center;
        font-family: 'Times New Roman', Times, serif;
        font-size: 30px;
        font-weight: bold;">用户管理
    </div>
    <div>
      <el-button type="text" @click="dialogFormVisible = true">新建</el-button>
      <el-autocomplete
        width="100px"
        v-model="state"
        :fetch-suggestions="querySearchAsync"
        placeholder="按关键字搜索"
        @select="handleSelect"
      ></el-autocomplete>
      <el-button
        style="position: absolute; right: 10px; top: 128px"
        type="warning"
        size="small"
        @click="dialogFormVisible = true"
        >撤销</el-button
      >
    </div>

    <el-dialog title="新建/编辑用户" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <div style="width: 296px">
          <el-form-item label="姓名" :label-width="formLabelWidth">
            <el-input
              v-model="form.name"
              autocomplete="off"
              placeholder="请输入内容"
            ></el-input>
          </el-form-item>
        </div>
        <div style="width: 296px">
          <el-form-item label="联系电话" :label-width="formLabelWidth">
            <el-input
              v-model="form.phone"
              autocomplete="off"
              placeholder="请输入联系电话"
            ></el-input>
          </el-form-item>
        </div>
        <div style="width: 296px">
          <el-form-item label="年龄" :label-width="formLabelWidth">
            <el-input
              v-model="form.age"
              autocomplete="off"
              placeholder="请输入年龄"
            ></el-input>
          </el-form-item>
        </div>
        <el-form-item label="性别" :label-width="formLabelWidth">
          <el-cascader
            v-model="form.sex"
            :options="optionss"
            clearable
          ></el-cascader>
        </el-form-item>
        <el-form-item label="详细地址" :label-width="formLabelWidth">
          <el-cascader
            v-model="form.address"
            :options="options"
            clearable
            @change="handleChange"
          ></el-cascader>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="handleAdd"
          >确 定</el-button
        >
      </div>
    </el-dialog>
    <el-table :data="tableData" border-style="width:100%" @selection-change="handleSelectionChange">
      <el-table-column type="selection" width="55" > </el-table-column>
      <el-table-column
        fixed
        prop="name"
        label="姓名"
        width="180"
      ></el-table-column>
      <el-table-column prop="age" label="年龄" width="180"> </el-table-column>
      <el-table-column prop="phone" label="联系电话" width="250">
      </el-table-column>
      <el-table-column prop="sex" label="性别" width="180"> </el-table-column>
      <el-table-column prop="address" label="详细地址" width="800">
      </el-table-column>

      <el-table-column fixed="right" label="  操作" width="220">
        <template slot-scope="scope">
          <div style="display: flex; padding-right: 5px">
            <el-button size="mini" @click="handleEdit(scope.$index, scope.row)"
              >编辑</el-button
            >
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
              >删除</el-button
            >
          </div>
        </template>
      </el-table-column>
    </el-table>
    <div>
      <el-button
        size="mini"
        type="danger"
        @click="handleDeletes"
        >批量删除</el-button
      >
    </div>

    <div class="block" style="text-align: center">
      <span class="demonstration">对咱们这页面评分</span>
      <el-rate v-model="value2" :colors="colors"> </el-rate>
    </div>
  </div>
</template>
<script>
export default {
  created() {
    let demo = localStorage.getItem("demo");
    if (demo) {
      this.tableData = JSON.parse(demo).data;
    } else {
      let data = [
        {
          id:new Date().getTime(),
          name: "佘冬键",
          phone: "123456789",
          sex: "男",
          address: "天河区",
          age: 22,
        },
        {
          id:new Date().getTime(),
          name: "佘冬键",
          phone: "123456789",
          sex: "男",
          address: "天河区",
          age: 22,
        },
        {
          id:new Date().getTime(),
          name: "佘冬键",
          phone: "123456789",
          sex: "男",
          address: "天河区",
          age: 22,
        },
        {
          id:new Date().getTime(),
          name: "佘冬键",
          phone: "123456789",
          sex: "男",
          address: "天河区",
          age: 22,
        },
      ];
      localStorage.setItem("demo", JSON.stringify({ data }));
      this.tableData = data;
    }
  },
  methods: {
    handleSelectionChange(e){
      this.choseList = e.map((item) =>{
        return item.id
      })
      console.log(e)
    },
    handleChange(value) {
      console.log(value)
    },
    handleClick(row) {
      console.log(row);
      this.save();
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.dialogFormVisible = true;
      this.save();
    },
    handleDelete(index, row) {
      this.tableData.splice(index, 1);
      console.log(index, row);
      this.save();
    },
    handleDeletes() {
      this.tableData = this.tableData.filter((item) =>{
        return !this.choseList.includes(item.id)
      })
      this.save();
    },
    handleAdd() {
      this.tableData.push(this.form);
      this.dialogFormVisible = false
       this.save();
    },
    save(){
      localStorage.setItem("demo", JSON.stringify({ data:this.tableData }));
    },
    querySearchAsync() {},
    handleSelect() {}
  },
  data() {
    return {
      restaurants: [],
      state: "",
      timeout: null,
      value1: null,
      value2: null,
      colors: ["#99A9BF", "#F7BA2A", "#FF9900"], // 等同于 { 2: '#99A9BF', 4: { value: '#F7BA2A', excluded: true }, 5: '#FF9900' }

      input: "",
      tableData: [],
      dialogTableVisible: false,
      dialogFormVisible: false,
      form: {
        name: "",
        phone:"",
        age:"",
        sex:"",
        address:""

      },
      formLabelWidth: "80px",
      options: [
        {
          value: "广东省",
          label: "广东省",
          children: [
            {
              value: "广州市",
              label: "广州市",
              children: [
                {
                  value: "天河区",
                  label: "天河区",
                },
                {
                  value: "番禺区",
                  label: "番禺区",
                },
                {
                  value: "荔湾区",
                  label: "荔湾区",
                },
                {
                  value: "黄浦区",
                  label: "黄浦区",
                },
              ],
            },
          ],
        },
      ],
      optionss: [
        {
          value: "男",
          label: "男",
        },
        {
          value: "女",
          label: "女",
        },
      ],
      choseList: ''
    };
  },
};
</script>
<style>
</style>