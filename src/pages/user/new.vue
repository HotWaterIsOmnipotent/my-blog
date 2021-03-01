<template>
  <Layout>
    <div style="min-height: 600px" v-loading="loading">
      <el-card shadow="never" style="min-height: 400px" v-if="$page.blog.edges[0].node.id">
        <div slot="header">
          <span>{{ $page.blog.edges[0].node.title }}</span>
        </div>
        <div style="font-size: 0.9rem; line-height: 1.5; color: #606c71">
          发布 {{ $page.blog.edges[0].node.created_at }} <br />
          更新 {{ $page.blog.edges[0].node.published_at }}
        </div>
        <div
          style="
            font-size: 1.1rem;
            line-height: 1.5;
            color: #303133;
            border-bottom: 1px solid #e4e7ed;
            padding: 5px 0px 5px 0px;
          "
        >
          <pre style="font-family: '微软雅黑'">{{ $page.blog.edges[0].node.description }}</pre>
        </div>
        <div
				v-html="md.render($page.blog.edges[0].node.content)"
          class="markdown-body"
          style="padding-top: 20px"
        ></div>
      </el-card>
      <el-card
        shadow="never"
        style="
          margin-bottom: 20px;
          padding: 20px 0px 20px 0px;
          text-align: center;
        "
        v-if="!$page.blog.edges[0].node.id"
      >
        <font style="font-size: 30px; color: #dddddd">
          <b>没有更新 ╮(๑•́ ₃•̀๑)╭</b>
        </font>
      </el-card>
    </div>
  </Layout>
</template>
<page-query>
query {
  blog: allStrapiPost {
    edges {
      node {
				id,
        title,
        content,
        published_at,
        created_at
      }
    }
  }
	
	general: allStrapiGeneral {
		edges {
			node {
				id,
				title,
				subtitle,
				image {
					url
				}
			}
		}
	}
}
</page-query>
<script>
import MarkdownIt from 'markdown-it';
export default {
  data() {
    return {
      query: {
        page: 1,
        pageSize: 1,
      },
      loading: false,
md : new MarkdownIt()

      // blog: {
      //   id: "",
      //   title: "",
      //   content: "",
      //   description: "",
      //   createTime: "",
      //   updateTime: "",
      // },
    };
  },
};
</script>