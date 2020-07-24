<template>
  <!-- 当form中只有一个输入框时，在此输入框中按下回车键即提交表单，如果希望阻止这一行为可以在el-form中使用@submit.native.prevent -->

  <el-form @submit.native.prevent="saveArticle" ref="form" :model="article" label-width="80px">
    <el-form-item label="文章标题">
      <el-input v-model="article.title"></el-input>
    </el-form-item>
    <el-form-item label="文章内容">
      <el-input type="textarea" v-model="article.body"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" native-type="submit">立即创建</el-button>
      <el-button>取消</el-button>
    </el-form-item>
  </el-form>
</template>
<script>
export default {
  data() {
    return {
      article: {},
    };
  },
  created() {
    // this.$http.get().then((res) => {
    //   console.log(res.data);
    // })
  },
  methods: {
    saveArticle() {
      this.$http.post("articles", this.article).then((res) => {
        if (res) {
          this.$message({
            type: "success",
            message: "文章创建成功",
          });
          this.$router.push("/articles/index");
        }
      });
    },
  },
};
</script>
