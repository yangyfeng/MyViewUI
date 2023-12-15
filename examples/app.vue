<template>
  <div class="container">
    <div class="router">
      <span
        :class="{ active: route.path === $route.path }"
        v-for="route in routes"
        :key="route.path"
        ><router-link :to="route.path">{{ route.name }}</router-link></span
      >
    </div>
    <div class="router-view">
      <router-view></router-view>
    </div>
  </div>
</template>
  <script>
module.exports = {
    data: function () {
        return {
            routes: [],
        };
    },
    mounted: function () {
        this.routes = this.$router.options.routes.map(({ path }) => {
            return {
                name: this.toCamelCase(path.replace('/', '')),
                path,
            };
        });
    },
    beforeDestroy: function () {},
    methods: {
        toCamelCase(input) {
            return input
        .split('-')
        .map((word) => word.charAt(0).toUpperCase() + word.slice(1))
        .join('');
        },
    },
};
</script>
  <style lang="less">
@import "../src/styles/index.less";
.container {
  width: 1366px;
  margin: 0 auto;
}
.router {
  margin: 0 auto;
  width: 1000px;
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 20px;
  border-bottom: 1px solid #ccc;
}
.router > span {
  display: block;
  width: 100px;
  padding: 5px;
}
.router-link-active {
  color: red;
}
.router-view {
  margin: 50px auto;
}
</style>