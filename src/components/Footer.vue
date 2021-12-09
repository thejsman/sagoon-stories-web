<template>
  <div class="footer-main">
    <a
      href="https://itunes.apple.com/us/app/sagoonlite/id1449566264?mt=8"
      target="_blank"
    >
      <img
        src="https://cdn.sagoon.com/common/common/app_store_29th.svg"
        alt=""
      />
    </a>

    <a
      href="https://play.google.com/store/apps/details?id=com.sagoonlite&referrer=utm_source%3Dsagoonlite%26utm_medium%story%26utm_term%3Dnonlogin"
      target="_blank"
    >
      <img
        src="https://cdn.sagoon.com/common/common/google_play_29th.svg"
        alt=""
      />
    </a>
  </div>
</template>
<style scoped>
.footer-main {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: #fff;
  text-align: center;
  z-index: 100;
  padding: 8px 16px;
}
.footer-main a {
  display: inline-block;
  margin: 0 5px;
}

@media screen and (max-width: 512px) {
  .footer-main {
    border-top: 1px solid rgba(0, 0, 0, 0.6);
  }
}
</style>
<script>
export default {
  name: "Footer",
  props: {
    msg: String,
  },
};
</script>
