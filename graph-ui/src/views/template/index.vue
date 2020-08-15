/** 模板 */
<template>
  <div class="com-html">
    <el-tabs v-model="activeName" tab-position="left">
      <el-tab-pane name="base" label="基础模板">
        <code-copy path="static/template/base.vue" />
      </el-tab-pane>

      <el-tab-pane name="temp-table" label="表格模板">
        <temp-table />
        <code-copy path="static/template/table.vue" />
        <!-- <el-collapse :v-model="['1']">
          <el-collapse-item title="表格代码展示" name="1">
            <code-copy path="static/template/table.vue" />
          </el-collapse-item>
        </el-collapse> -->
      </el-tab-pane>

      <el-tab-pane label="角色管理">角色管理</el-tab-pane>
      <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import codeCopy from '@/components/code/code-copy'
import tempTable from './components/table.vue'
export default {
  components: {
    codeCopy,
    tempTable
  },
  props: {},
  data() {
    return {
      activeName: 'temp-table'
    }
  },
  computed: {},
  created() {},
  mounted() {},
  methods: {
  }
}
</script>

<style lang="scss" scoped>
  .com-html {
    padding: 20px 20px 0;
  }
</style>

