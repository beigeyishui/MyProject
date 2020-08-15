/** 代码展示复制模板 */
<template>
  <div class="com-html">
    <button ref="btn" class="copy" :data-clipboard-text="code" data-clipboard-action="copy">
      复制
    </button>
    <div v-highlight>
      <pre>
        <code>{{ code }}</code>
      </pre>
    </div>
  </div>
</template>

<script>
import ClipboardJS from 'clipboard'

export default {
  components: {},
  props: {
    path: {
      type: String,
      default: null
    }
  },
  data() {
    return {
      code: ''
    }
  },
  beforeCreate() {
  },
  created() {
    if (this.path) {
      this.code = this.readFile(this.path)
    }
  },
  mounted() {
    this.copy()
  },
  methods: {
    copy() {
      const _this = this
      const clipboard = new ClipboardJS(this.$refs.btn)
      clipboard.on('success', function() {
        _this.$message.success('复制成功')
      })
      clipboard.on('error', function() {
        _this.$message.error('复制失败')
      })
    },
    readFile(filePath) {
      // 创建一个新的xhr对象
      let xhr = null
      if (window.XMLHttpRequest) {
        xhr = new XMLHttpRequest()
      } else {
      // eslint-disable-next-line
      xhr = new ActiveXObject('Microsoft.XMLHTTP')
      }
      const okStatus = document.location.protocol === 'file' ? 0 : 200
      xhr.open('GET', filePath, false)
      xhr.overrideMimeType('text/html;charset=utf-8')
      xhr.send(null)
      return xhr.status === okStatus ? xhr.responseText : null
    }
  }
}
</script>

<style lang="scss" scoped>
  .com-html {
    position: relative;
    .copy {
      cursor: pointer;
      position: absolute;
      right: 5px;
      top: 20px;
    }
  }
</style>

