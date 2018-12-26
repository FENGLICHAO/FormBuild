<template>
  <div class="home">
    <!--<div class="menu">
      <span>文本框</span>
    </div>
    <div class="content">

    </div>
    <div class="operation">

    </div>-->
    <Head></Head>
    <fm-making-form :data="jsonData"
                    generate-code
                    :remote="remoteFuncs"
                    :value="values"
                    ref="generateForm">
      <template slot="action">
        <!--<span @click="getHtml" class="get">getHtml</span>-->
        <span @click="getJSON" class="get">getJSON</span>
        <!--<span @click="getData" class="get">getData</span>-->
      </template>
    </fm-making-form>
  </div>
</template>
<style lang="less" scoped>
  .home {
    width:100%;
    height:100%;
    /*display:flex;*/
    /*flex-flow: column;*/
    /*.menu{
      width:20%;
      height:100%;
      display:flex;
      display:-webkit-box;
      border-right:1px solid #17A6B5;
      span{
        cursor: pointer;
        padding:5px 10px;
        background-color: #17A6B5;
        margin:10px;
        border-radius:8px;
      }
    }
    .content{
      width:50%;
      !*height:100%;*!
      border-right:1px solid #17A6B5;
      padding:0 10px;
    }
    .operation{
      width:30%;
      !*height:100%;*!
      !*background-color: #0B0B0B;*!
    }*/
  }
</style>
<script>
import Head from '../components/Head.vue'
export default {
  components: {
    Head
  },
  data () {
    return {
      jsonData: {}, // 表单配置中生成的json数据
      values: {}, // 表单需要显示的表单数据
      remoteFuncs: {
        // 组件配置时配置的远端方法,保持和配置时输入的名称一致
        func_test (resolve) {
          // 模拟接口请求
          setTimeout(() => {
            const options = [
              {id: '1', name: '1111'},
              {id: '2', name: '2222'},
              {id: '3', name: '3333'}
            ]

            // 获取到的值和标签可以通过配置页远端配置
            // 值:id  标签：name

            resolve(options) // 将后端获取的数据放入回调函数中
          }, 2000)
        }
      }
    }
  },
  methods: {
    getHtml (data, on) {
      // 同步调用
      let html = this.$refs.generateForm.getHtml()
      console.log(html)
    },
    getJSON () {
      // 同步调用
      let json = this.$refs.generateForm.getJSON()
      // console.log(json, this.jsonData)
      this.$router.push({
        name: 'test',
        params: {
          data: json
        }
      })
    },
    getData () {
      // 异步调用
      this.$refs.generateForm.getData().then(data => {
        // 数据校验成功
        // data 为获取的表单数据
        console.log(data)
      }).catch(e => {
        // 数据校验失败
      })
    }
  }
}
</script>
