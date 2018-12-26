<template>
  <div>
    <fm-generate-form :data="jsonData" :remote="remoteFuncs" :value="editData" ref="generateForm">

    </fm-generate-form>
    <el-button type="primary" @click="handleSubmit">提交</el-button>
  </div>
</template>
<script>/* eslint-disable */
  export default{
  data () {
    return {
      jsonData: {},
      editData: {},
      remoteFuncs: {

      }
    }
  },
  methods: {
    handleSubmit () {
      this.$refs.generateForm.getData().then(data => {
        // 数据校验成功
        // data 为获取的表单数据
      }).catch(e => {
        // 数据校验失败
      })
    }
  },
    mounted(){
      this.jsonData=this.$route.params.data
    }
}
</script>
