<template>
  <Layout>
    <div class="journal">
      <div class="container journal-container">

        <div class="journal-header">
          <h1 v-html="$page.post.title" class="journal-title" />
          <div class="journal-meta">
            <div class="journal-author">
              <span class="label">Author</span>
              <span class="author-name" v-text="$page.post.author" />
            </div>
            <div class="journal-date">
              <span class="label">Date</span>
              <div v-text="$page.post.updated_at"/>
            </div>
          </div>          
        </div>
        
        <g-image
            v-if="$page.post.cover_url"
            :src="$page.post.cover_url"
            :alt="$page.post.title"
            class="thumbnail"
        />

        <JournalContent :content="$page.post.content" />

      </div>
    </div>
  </Layout>
</template>

<page-query>
query strapiPost ($id: String!) {
  post: strapiPost (id: $id) {
    title
    cover_url
    updated_at
    content
  }
}
</page-query>

<script>
import JournalContent from "@/components/JournalContent"

export default {
  components: {
    JournalContent
  },
  metaInfo () {
    return {
      title: this.$page.post.title
    }
  }
}
</script>

<style scoped>
.journal-container {
  max-width: 840px;
}
.journal-header {
  padding: 2rem 0 4rem 0;
}
.journal-title {
  font-size: 4rem;
  margin: 0 0 4rem 0;
  padding: 0;
}
.journal-meta {
  display: flex;
  flex-wrap: wrap;
  font-size: 0.8rem;
}
.journal-meta > div {
  margin-right: 4rem;
}
.journal-meta > div:last-of-type {
  margin: 0;
}
.thumbnail {
  height: 560px;
  object-fit: cover;
  transition: all 0.15s ease;
  box-shadow: 0 0 40px -20px rgba(0,0,0,0.25);
  margin-bottom: 10px;
}
</style>
