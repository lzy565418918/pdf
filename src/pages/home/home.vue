<template>
  <div>
    <div class="title">{{msg}}</div>
    <pdf />
  </div>
</template>
<script>
import pdf from '@/components/pdf.vue'
export default {
  props: {
    msg: {
      type: String,
      default: () => {}
    }
  },
  //import引入的组件需要注入到对象中才能使用
  components: {
      pdf
  },
  data() {
    //这里存放数据
    return {};
  },
  //监听属性 类似于data概念
  computed: {},
  //监控data中的数据变化
  watch: {},
  //方法集合
  methods: {},
  //生命周期 - 创建完成（可以访问当前this实例）
  created() {},
  //生命周期 - 挂载完成（可以访问DOM元素）
  mounted() {}
};
</script>
<style lang='less' scoped>
</style>