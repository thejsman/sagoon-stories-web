<template>
  <div class="header">
    <div class="header-center">
      <a href="https://www.sagoonlite.com/" class="logo">
        <img
          width="120"
          alt="sagoon Lite"
          src="https://cdn.sagoon.com/common/common/sagoon_logo.svg"
        />
      </a>
    </div>
  </div>
</template>
<style scoped>
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 60px;
  background-color: #ffffff;
  color: white;
  font-weight: 600;
  box-shadow: 0px 1px 2px rgba(0, 0, 0, 0.34);
  z-index: 1000;
}
.header img {
  margin: 16px 16px;
}
.header-center {
  margin: 0 auto;
  max-width: 768px;
  text-align: center;
}
.logo {
  display: inline-block;
}

/* .log-in {
  float: right;
  display: inline-block;
  margin: 20px 16px;
} 
.log-in a {
  text-decoration: none;
  color: #4440c7;
}*/
</style>
<script>
export default {
  name: "Header",
  props: {
    msg: String,
  },
};
</script>
