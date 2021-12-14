<template>
  <div id="app">
    <Header />
    <Story :story="storyTop" />
    <Footer />
  </div>
</template>

<script>
import Footer from "./components/Footer.vue";
import Story from "./components/story-component.vue";
import Header from "./components/Header.vue";
import Vue from "vue";
import { BootstrapVue, BootstrapVueIcons } from "bootstrap-vue";
import axios from "axios";
Vue.use(BootstrapVue);
Vue.use(BootstrapVueIcons);
export default {
  name: "App",
  components: {
    Header,
    Footer,
    Story,
  },
  data() {
    return {
      storyTop: [],
      storyAll: [],
      storyId: "",
    };
  },
  async created() {
    const urlParams = new URL(location.href).searchParams.get("story");
    this.storyId = urlParams;
    if (urlParams && urlParams !== null) {
      if (urlParams.length) {
        await this.getStory(urlParams);
      }
    } else {
      // await this.getAllStory();
    }
  },
  methods: {
    async getStory(storyId) {
      try {
        const result = await axios.get(
          `https://bt4a37ws83.execute-api.ap-southeast-1.amazonaws.com/live/story/detail/${storyId}?Utm-Campaign-Id=iFLXGq9j82DnzWQyd8s9SoTVX3cpDzTc`,
          {
            headers: {
              "Content-Type": "application/json",
              "Utm-Campaign-Id": "iFLXGq9j82DnzWQyd8s9SoTVX3cpDzTc",
            },
          }
        );

        this.storyTop = result.data.secrets;
        // await this.getAllStory();
      } catch (error) {
        console.log("Error in get story: ", { error });
        this.storyTop = [];
        // await this.getAllStory();
      }
    },
    async getAllStory() {
      try {
        const result = await axios.get("./story-second.json");
        this.storyAll = result.data.secrets;
        if (this.storyTop !== undefined) {
          this.storyTop = this.storyTop.concat(this.storyAll);
        } else {
          this.storyTop = [...this.storyAll];
        }
      } catch (error) {
        console.log("Error in get storyAll: ", { error });
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: rgba(0, 0, 0, 0.87);
  margin-top: 80px;
  padding-bottom: 100px;
}
@import "~bootstrap-vue/dist/bootstrap-vue.css";
@import "~bootstrap/dist/css/bootstrap.css";
@import "assets/style.css";
</style>
