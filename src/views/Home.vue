<template>
  <div class="home">
    <Navbar />
    <div class="columns">
      <div class="abs"></div>
      <div class="column is-8 is-offset-4 mt-6">
        <p
          class="has-text-info is-size-2 has-text-weight-bold is-family-primary mt-5"
        >
          Find the best movies now !
        </p>
        <span class="has-text-grey">
          Lorem ipsum dolor sit, amet consectetur adipisicing elit. Velit,
          delectus nostrum aperiam sint tempora soluta autem nulla adipisci
          illum temporibus nihil neque, ipsa similique corrupti?
        </span>

        <section class="mt-3 pr-6 box-card">
          <b-field>
            <b-input v-model="keyword" placeholder="Search"></b-input>
          </b-field>
          <div class="columns">
            <div class="column">
              <div
                class="card mb-5 card-hover"
                v-for="(data, i) in info"
                :key="i"
              >
                <router-link :to="data.show.officialSite" target="_blank">
                  <div
                    @click="link(data.show.officialSite)"
                    class="card-content has-text-black"
                  >
                    <div class="media">
                      <div class="media-left">
                        <figure class="image is-48x48">
                          <img
                            :src="data.show.image.medium"
                            alt="Placeholder image"
                          />
                        </figure>
                      </div>
                      <div class="media-content">
                        <p class="title is-4">{{ data.show.name }}</p>
                        <p class="subtitle is-6 mb-0">
                          Rating : {{ data.show.rating.average }}
                        </p>
                        <b-tag
                          class="is-info mt-2 mr-2"
                          v-for="(b, tg) in data.show.genres"
                          :key="tg"
                        >
                          {{ b }}
                        </b-tag>
                      </div>
                    </div>
                    <div class="content pt-3" v-html="data.show.summary"></div>
                  </div>
                </router-link>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Navbar from "@/components/Navbar.vue";

export default {
  name: "Home",
  components: {
    Navbar,
  },
  data() {
    return {
      view: false,
      info: [],
      keyword: "",
      data: [],
    };
  },
  watch: {
    keyword: "search",
  },
  methods: {
    showBtn() {
      this.view = true;
      // console.log(this.info);
    },
    search() {
      axios
        .get(`http://api.tvmaze.com/search/shows?q=${this.keyword}`)
        .then((res) => (this.info = res.data));

      console.log("data", this.info);
    },
  },
};
</script>

<style scoped>
.abs {
  position: fixed;
  height: 100vh;
  top: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: red;
}
.card-hover:hover {
  box-shadow: 0 0 35px -10px;
}

.abs {
  background-image: url("https://images.unsplash.com/photo-1575727735640-ed79e28955d8?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=408&q=80");
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  width: 350px;
  object-fit: contain;
}
</style>
