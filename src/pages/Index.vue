<template>
  <Layout>

    <div class="container">
      <div class="index-title">
        <h1>{{this.general.title}}</h1>
        <h2>{{this.general.subtitle}}</h2>
      </div>

      <div class="projects">
        <div class="project" v-for="item in this.mainList" :key="item.node.id">
          <g-link>
            <img :src="`http://113.31.155.103:1337${item.node.url[0].url}`" alt="">
            <h3>{{item.node.title}}</h3>
            <div class="categories">
              <span class="category" v-for="cate in item.node.category" :key="cate.name">{{cate.name}}</span>
            </div>
          </g-link>
        </div>
      </div>
    </div>

    <div class="journals">
      <div class="journals-heading">Latest and greatest</div>
      <div class="journals-lists">
        <div class="journal-container">
          <g-link v-for="item in this.posts" :key="item.node.id">{{item.node.title}}</g-link>
        </div>
      </div>
    </div>
    <footer>
      <span>Copyright © 2021</span>
    </footer>
  </Layout>
</template>

<page-query>
query {
  general: allStrapiMySiteGeneral {
    edges {
      node {
        title
        subtitle
      }
    }
  }

  mainList: allStrapiMains {
    edges {
      node {
        id
        title
        url {
          url
        }
        category {
          name
        }
      }
    }
  }

  posts: allStrapiPost {
    edges {
      node {
        id
        title
        content
				created_at
      }
    }
  }
}
</page-query>

<script>
export default {
  metaInfo: {
    title: 'Hello, world!'
  },
  computed: {
    general () {
      return this.$page.general.edges[0].node
    },
    mainList () {
      return this.$page.mainList.edges
    },
    posts () {
      return this.$page.posts.edges
    }
  }
}
</script>

<style>
a {
  text-decoration: none;
}
.container {
  /* width: 100%; */
  margin: 0 auto;
  padding: 0 6rem;
}
.index-title {
  width: 480px;
  margin: 0 auto;
}
.index-title h1 {
  font-size: 3rem;
  font-weight: 700;
  padding: 0;
  margin: 0 0 2rem;
  text-align: center;
}
.index-title h2 {
  font-size: 1.15em;
  font-weight: 400;
  line-height: 1.68;
  opacity: 0.6;
  text-align: center;
}
.projects {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 4rem;
}

.project {
  grid-column: auto/span 1;
  text-align: center;
  /* height: 300px;
  background: yellowgreen; */
}

.project:nth-child(3n + 1) {
  grid-column: auto/span 2;
}

.project img {
  width: 100%;
  height: 560px;
  object-fit: cover;
  transition: transform 0.3s;
}

.project img:hover {
  transform: scale(1.05);
}

.project h3 {
  font-size: 1rem;
  color: #333;
  margin: 2rem 0 1rem;
}

.categories {
  text-align: center;
  font-size: 0.8rem;
  color: #2b2b2b;
}

.category {
  margin: 0 0.4rem;
}

.journals-heading {
  margin-top: 6rem;
  margin-bottom: 1rem;
  font-size: 0.6rem;
  font-weight: 400;
  text-transform: uppercase;
}

.journal-container {
  display: flex;
  width: 1200px;
  margin: 0 atuo;
}

.journal-container a {
  flex: 1;
  display: block;
  padding: 2rem;
  /* transition: background 0.25s ease; */
  text-decoration: none;
  font-size: 1rem;
  font-weight: 400;
  color: #333;
}

.journal-container a:hover {
  background-color: rgba(0, 0, 0, 0.2);
}

footer {
  font-size: 0.8rem;
  padding: 6rem 0;
}
</style>
