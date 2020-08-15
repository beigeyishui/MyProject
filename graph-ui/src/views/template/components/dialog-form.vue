/** 弹出框表单 */
<template>
  <div>
    <el-dialog
      append-to-body
      :title="message[status].title"
      :visible.sync="visible"
      class="dialog-main"
      top="5%"
      width="400px"
      destroy-on-close
      :close-on-click-modal="false"
    >
      <el-form ref="form" :model="form" :rules="rules">
        <el-form-item label="名称">
          <el-input v-model="form.name" placeholder="请入如名称" />
        </el-form-item>
      </el-form>
      <span slot="footer">
        <el-button @click="visible = false">取 消</el-button>
        <el-button type="primary" @click="submit">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>
export default {
  components: { },
  props: { },
  data() {
    return {
      visible: false,

      status: 0, // 0添加 1修改
      message: [
        { title: '添加表单', url: '/rwAnnual/add' },
        { title: '修改表单', url: '/rwAnnual/update' }
      ],

      // 表单隐藏字段
      param: {},
      // 表单填写字段
      form: {
        name: ''
      },

      rules: {
        name: [
          { required: true, message: '请输入名称' }
        ]
      }
    }
  },
  computed: {

  },
  created() {
    this.visible = false
  },
  mounted() {
    // console.log(this.label)
  },
  methods: {
    // 打开弹框
    openDialog(row, params) {
      this.visible = true
      if (row) { // 修改
        this.status = 1

        this.param = {
          id: row.id
        }

        this.form = {
          name: row.name
        }
      } else { // 添加
        this.status = 0

        this.param = params || {}

        this.form = {
          name: ''
        }

        this.ruleForm = {
          annualId: ''
        }
        this.resetForm('form')
      }
    },
    submit() {
      // const url = this.message[this.status].url
      // const params = this.ruleForm
      // baseRequest(url, params).then(() => {
      //   this.visible = false
      //   this.$emit('refresh')
      // })
    },
    resetForm(formName) {
      // 对整个表单进行重置，将所有字段值重置为初始值并移除校验结果
      this.$refs[formName].resetFields()
    }
  }
}
</script>
<style lang="scss" scoped>

</style>
