/** 表格模板 */
<template>
  <div>
    <el-table
      :data="tableData"
      style="width: 100%"
    >
      <el-table-column prop="date" label="日期" width="180" />
      <el-table-column prop="name" label="姓名" width="180" />
      <el-table-column prop="address" label="地址" />
      <el-table-column>
        <template slot="header" slot-scope="scope">
          <el-button size="mini" type="primary" @click="addRow(scope.row)">添加</el-button>
        </template>
        <template slot-scope="scope">
          <el-link type="primary" @click="updateRow(scope.row)">{{ scope.$index }}. 修改</el-link>
        </template>
      </el-table-column>
      <el-table-column label="操作" align="center" width="180">
        <template slot-scope="scope">
          <el-button size="mini" type="danger" plain @click="deleteRow(scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      :current-page="pageNo"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
    />
    <dialog-form ref="form" @refresh="refresh" />
  </div>
</template>

<script>
import dialogForm from './dialog-form'
export default {
  components: {
    dialogForm
  },
  props: { },
  data() {
    return {
      // 表格数据
      tableData: [],
      // 分页
      pageNo: 1,
      pageSize: 10,
      total: null
    }
  },
  computed: { },
  created() {
    this.searchOption()
  },
  mounted() { },
  methods: {
    // 查询数据
    searchOption(page) {
      if (!page) {
        this.pageNo = 1
      }

      this.tableData = [
        { date: '2016-05-02', name: '王小虎', address: '上海市普陀区金沙江路 1518 弄' },
        { date: '2016-05-02', name: '王小虎', address: '上海市普陀区金沙江路 1518 弄' },
        { date: '2016-05-02', name: '王小虎', address: '上海市普陀区金沙江路 1518 弄' }
      ]
      this.total = 100
    },
    // 添加数据
    addRow() {
      console.log('add')
      this.$refs.form.openDialog()
    },
    // 修改数据
    updateRow(row) {
      console.log('update', row)
      this.$refs.form.openDialog(row)
    },
    // 删除数据
    deleteRow(row) {
      console.log('delete', row)
      this.$message.error('删除失败')
    },
    // 刷新表格
    refresh() {
      this.$message.success('表格刷新')
    },
    // 分页
    handleSizeChange(val) {
      this.pageSize = val
      this.searchOption()
    },
    // 分页
    handleCurrentChange(val) {
      this.pageNo = val
      this.searchOption(true)
    }
  }
}
</script>

<style lang="scss" scoped>

</style>

