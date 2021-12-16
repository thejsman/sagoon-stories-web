<template>
  <div class="card-secret-main">
    <div class="card secret-card" v-for="(secret, index) in story" :key="index">
      <div class="card-header">
        <div class="media">
          <div class="media-left">
            <a href="#" class="dspl-inline">
              <span class="btn-floating">
                <img
                  v-bind:src="secret.created_by.profile_image"
                  @error="imgPlaceholder"
                  class="img-fluid"
                />
              </span>
            </a>
            <span class="profile-name">
              {{ secret.created_by.full_name }}
            </span>
            <div class="secret-category">
              <span class="secret-type" v-if="secret.topics[0].id == 0">
                My Circle
              </span>
              <span class="secret-type" v-if="secret.topics[0].id != 0">
                {{ secret.topics[0].topic }}
              </span>
            </div>
          </div>

          <!-- <div class="media-body"></div>
          <div class="media-right">
            <div class="dropdown dropdown-menu-end">
              <button
                class="btn btn-link dropdown-toggle"
                type="button"
                id="dropdownMenuButton1"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                <i class="zmdi zmdi-more"></i>
              </button>
              <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                <li><a class="dropdown-item" href="#">Link</a></li>
              </ul>
            </div>
          </div> -->
        </div>
      </div>

      <div
        class="card-content"
        v-bind:class="getColorCode(secret)"
        v-if="secret.url_info == null"
      >
        <div class="card-image" v-if="secret.secret_img.length > 0">
          <div
            class="fig-holder"
            v-for="item in secret.secret_img"
            :key="item.secretImg"
          >
            <img
              v-bind:src="item.thumbnail"
              class="img-fluid"
              data-bs-toggle="modal"
              data-bs-target="#content"
              @click="
                activeImageUrl = {
                  url: item.url,
                  thumbnail: item.thumbnail,
                  type: item.type,
                }
              "
            />
            <i
              class="zmdi zmdi-play-circle-outline zmdi-hc-fw ply-btn"
              v-if="item.type == 'video/mp4' || item.type == 'video'"
            ></i>

            <!-- Modal -->
            <div
              class="modal fade"
              id="content"
              tabindex="-1"
              aria-labelledby="contentLabel"
              aria-hidden="true"
            >
              <div class="modal-dialog modal-xl">
                <div class="modal-content">
                  <button
                    type="button"
                    class="btn-close"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                    @click="closeModal"
                  >
                    <i class="zmdi zmdi-close"></i>
                  </button>

                  <div class="modal-body">
                    <div
                      class="img-show"
                      v-if="
                        activeImageUrl.type === 'image/jpeg' ||
                          activeImageUrl.type === 'image'
                      "
                    >
                      <img
                        v-bind:src="activeImageUrl.thumbnail"
                        class="img-fluid"
                        v-bind:type="activeImageUrl.type"
                      />
                    </div>

                    <div
                      class="video-show"
                      v-if="
                        activeImageUrl.type === 'video/mp4' ||
                          activeImageUrl.type === 'video'
                      "
                    >
                      <video controls autoplay>
                        <source
                          v-bind:src="activeImageUrl.url"
                          v-bind:type="'video/mp4'"
                        />
                      </video>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="wrap_p">
          <p class="" v-bind:class="getContentLength(secret.content)">
            {{ secret.content }}
          </p>
          <p v-if="secret.color_codes.link">
            <a
              style="text-decoration: underline;"
              v-bind:href="secret.color_codes.link"
              target="_blank"
              >Read More</a
            >
          </p>
        </div>
      </div>

      <div class="card-content" v-if="secret.url_info !== null">
        <div class="wrap_p1">
          <div
            class="card-image single-fig"
            v-if="secret.url_info.image.length > 0"
          >
            <a
              v-bind:href="secret.url_info.original_url"
              v-bind:title="secret.url_info.title"
              target="_blank"
            >
              <div class="img-holder">
                <figure>
                  <img alt="story" v-bind:src="secret.url_info.image" />
                </figure>
              </div>
            </a>
          </div>

          <div class="url_info">
            <a
              v-bind:href="secret.url_info.original_url"
              v-bind:title="secret.url_info.title"
              target="_blank"
            >
              <p class="p-sm">
                <span>{{ secret.url_info.url }}</span>
              </p>
              <p class="p-md">
                <span>{{ secret.url_info.title }}</span>
              </p>

              <p class="p-md-l">
                <span>{{ secret.url_info.description }}</span>
              </p>
            </a>
          </div>
          <p v-if="secret.content">
            {{ secret.content }}
          </p>
          <!-- <p v-if="secret.content"><a v-bind:href="secret.content | parseUrl">{{ secret.content }}</a></p> -->
        </div>
      </div>

      <div class="activities-count">
        <div class="activity-sec">
          <a href="https://sagoonapp.app.link/fb-campaign" target="_blank">
            <figure>
              <img
                src="https://cdn.sagoon.com/common/common/favorite_border_black.svg"
                alt=""
              />
            </figure>
            <span>{{ secret.my_reaction }} Likes</span>
          </a>
        </div>

        <div class="activity-sec">
          <a href="https://sagoonapp.app.link/fb-campaign" target="_blank">
            <figure>
              <img
                src="https://cdn.sagoon.com/common/common/visibility_black.svg"
                alt=""
              />
            </figure>
            <span>{{ secret.total_view_count }} Views</span>
          </a>
        </div>

        <div class="activity-sec">
          <a href="https://sagoonapp.app.link/fb-campaign" target="_blank">
            <figure>
              <img
                src="https://cdn.sagoon.com/common/common/ios_share_black.svg"
                alt=""
              />
            </figure>
            <span>{{ secret.shared_count }} Share</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Story",
  props: {
    msg: String,
    story: {
      type: Array,
      default: () => [],
    },
  },
  async created() {},
  methods: {
    imgPlaceholder(e) {
      e.target.src = "https://cdn.sagoon.com/common/common/plc-15th.jpg";
    },
    closeModal() {
      this.activeImageUrl = { url: "", thumnail: "", type: "" };
    },
  },
  computed: {
    filteredItems() {
      if (this.storyId) {
        const filtered = this.secrets.filter(
          (secret) => secret.story_id === this.storyId
        );
        return filtered.length ? filtered : this.secrets;
      } else {
        return this.secrets;
      }
    },

    getColorCode() {
      return (secret) => {
        if (secret.color_codes && secret.color_codes.gradient_color_1) {
          return (
            "bg bg-" + secret.color_codes.gradient_color_1.replace("#", "")
          );
        } else {
          return "";
        }
      };
    },
    getContentLength() {
      return (content) => {
        if (content.length < 73) {
          return "onethirdtxt";
        } else if (content.length >= 73 && content.length < 146) {
          return "twothirdtxt";
        } else {
          return "fulltxt";
        }
      };
    },
    initSecretReaction() {
      return (secret) => {
        if (secret.my_reaction === 0) {
          secret.selectedReaction = secret.reactionsList[0];
        } else {
          secret.selectedReaction =
            secret.reactionsList[secret.my_reaction - 1];
        }
      };
    },
  },
  mounted() {},
  data() {
    return {
      storyId: null,
      secrets: [],
      activeImageUrl: { url: "", thumnail: "", type: "" },
      message: "",
      errors: "",
      page: "d8422aab1799444c946d.205",
      payment_method: "stripe",
    };
  },
};
</script>
