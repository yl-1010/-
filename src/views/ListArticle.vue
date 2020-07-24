<template>
  <div>
    <el-table :data="articles">
      // prop表示对应数据中字段的名称，label表示表头名称
      <el-table-column prop="title" label="标题" width="140"> </el-table-column>
      <el-table-column prop="body" label="内容" width="120"> </el-table-column>
      <el-table-column fixed="right" label="操作" width="100">
        <template slot-scope="scope">
          <el-button @click="edit(scope.row._id)" type="text" size="small">编辑</el-button>
          <el-button @click="del(scope.row._id)" type="text" size="small">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      articles: [],
    };
  },
  methods: {
    // 获取数据
    getInfo() {
      this.$http.get("articles").then((res) => {
        this.articles = res.data;
        console.log(res.data);
      });
    },
    edit(id) {
      console.log(id);
      this.$router.push(`/articles/${id}/edit`)
    },
    del(id) {
      this.$http.delete(`articles/${id}`).then((res) => {
        this.$message({
          type: "success",
          message: "删除成功",
        });
        console.log(res)
        this.getInfo();
      });
    },
  },
  created() {
    this.getInfo();
  },
};
</script>
