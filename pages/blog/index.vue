<template>
  <section class="container blog-page">
    <div class="main-header m-4">
      <h1>آخر المقالات</h1>
    </div>
    <div class="row loading" v-if="!isLoaded">
      <div class="text-center">جاري تحميل المقالات ....</div>
    </div>
    <div class="row">
      <div class="col-12 col-md-4 col-lg-3" v-for="post in posts" :key="post.id">
        <div class="card" style="width: 18rem;">
          <img :src="post.img" class="card-img-top" :alt="post.title" />
          <div class="card-body">
            <h5 class="card-title">{{post.title}}</h5>
            <p class="card-text">{{ post.excerpt}}</p>
            <a :href="post.link" target="_blank" class="btn btn-outline-dark">أكمل المقالة ..</a>
          </div>
        </div>
      </div>
    </div>
    <div class="row page-count" v-if="isLoaded">
      <div class="col-12">
        <div class="btn-group">
          <button @click="changePageNo(-1)" :disabled="firstPage" class="btn btn-secondary back">
            <i></i>
          </button>
          <button class="btn btn-secondary">{{pageNo}}</button>
          <button @click="changePageNo(1)" :disabled="lastPage" class="btn btn-secondary front">
            <i></i>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      isLoaded: false,
      posts: [],
      pageNo: 1,
      lastPage: false,
      firstPage: true
    };
  },
  methods: {
    changePageNo(val) {
      this.firstPage = true;
      this.lastPage = false;

      if (this.pageNo > 1) {
        this.firstPage = false;
      } else {
        this.firstPage = true;
      }

      if (this.pageNo > 0 && val == 1) {
        this.pageNo = this.pageNo + val;
        this.firstPage = false;
      }
      if (this.pageNo > 1 && val == -1) this.pageNo = this.pageNo + val;

      this.isLoaded = false;
      this.posts = [];
    },
    getData() {
      axios
        .get(
          `http://arab-wordpress.com/wp-json/wp/v2/posts?page=${this.pageNo}&per_page=12`
        )
        .then(res => {
          res.data.forEach((el, i) => {
            let post = [];
            post.id = el.id;
            post.title = el.title.rendered;
            post.link = el.link;
            post.excerpt =
              el.excerpt.rendered
                .split("<p>")[1]
                .split(" ")
                .splice(0, 20)
                .join(" ") + " ...";
            post.slug = el.slug;

            // get image
            axios
              .get(
                `http://arab-wordpress.com/wp-json/wp/v2/media/${el.featured_media}`
              )
              .then(imgres => {
                post.img = imgres.data.source_url;
                this.posts.push(post);
              });
          });
          this.isLoaded = true;
        });
    }
  },
  created() {
    this.getData();
  },
  watch: {
    pageNo: function() {
      this.getData();
    }
  },
  updated() {
    if (this.posts.length < 10) {
      this.lastPage = true;
    } else {
      this.lastPage = false;
    }
  }
};
</script>

<style scoped>
.card {
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.15);
  text-align: right;
  width: 100% !important;
  margin: 10px 0;
}
.card-title {
  font-size: 18px;
  font-weight: bold;
  line-height: 1.5;
}
.card-text {
  font-size: 14px;
}
.card-body .btn {
  width: 100%;
}
.loading div {
  width: 100%;
}
.btn-group {
  direction: ltr;
}
.btn-group i {
  display: inline-block;
  border: 2px solid #fff;
  border-top: none;
  border-left: none;
  width: 10px;
  height: 10px;
  border-radius: 2px;
  transform: rotate(135deg) translate(-2px, -2px);
}
.btn-group .front i {
  transform: rotate(-45deg) translate(-2px, -2px);
}
.page-count > div {
  display: flex;
  justify-content: center;
  padding-top: 20px;
}
</style>
