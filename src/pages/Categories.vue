<template>
  <Layout>
    <v-container :class="$style.topContainer">
      <v-container>
        <v-layout text-xs-center wrap>
          <v-flex xl12>
            <v-breadcrumbs class="justify-center" :items="items" divider=">"></v-breadcrumbs>
            <h1 :class="$style.text">Categories</h1>
          </v-flex>
        </v-layout>
      </v-container>
      <v-divider></v-divider>
      <v-container fluid grid-list-md>
        <v-layout row wrap>
          <v-flex v-for="tag in tagsContent" :key="tag.node.title" xs12 sm12 md4 lg3 xl2>
            <TagCard :tag="tag.node" />
          </v-flex>
        </v-layout>
      </v-container>
    </v-container>
  </Layout>
</template>

<page-query>
query {
  allContentfulTag {
    edges {
      node {
        title
        description
        coverImage {
          title
          file {
            url
          }
        }
      }
    }
  }
}
</page-query>

<script>
import TagCard from '../components/TagCard';

export default {
  metaInfo: {
    title: "Categories",
    meta: [
      {
        name: "description",
        content: "Various topics based on my blog posts and projects."
      }
    ]
  },
  data: () => ({
    items: [
      {
        text: "Home",
        disabled: false,
        href: "/"
      },
      {
        text: "Categories",
        disabled: false,
        href: "/categories/"
      }
    ]
  }),
  computed: {
    tagsContent() {
      return this.$page.allContentfulTag.edges;
    }
  },
  components: {
    TagCard
  }
};
</script>

<style module lang="css">
.topContainer {
  padding-top: 40px;
}

.text {
  color: #3f51b5;
  font-family: "Montserrat", "Helvetica Neue", Arial, sans-serif;
}
</style>
