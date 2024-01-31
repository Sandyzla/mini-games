<template>
  <div class="homePage">
    <h1>
      Choose Your Game!
    </h1>
    <label class="icon2048" @click="to2048">2048</label>
    <label class="iconThree" @click="toThree">Three!</label>
    <!-- <label class="iconDemo">链接
      <a href="https://www.baidu.com">百度</a>
    </label> -->
    <!-- <label class="iconDemo" @click="toDemo">demo</label> -->
  </div>
</template>

<script>

export default {
  name: 'App',
  methods: {
    to2048() {
      this.$router.replace('/2048');
    },
    toThree() {
      this.$router.replace('/three');
    },
    toDemo() {
      this.$router.replace('/demo');
    }
  }

}
</script>

<style scoped>
html {
  margin: 0;
  padding: 0;
}

h1 {
  margin: 0;
  height: 60px;
  padding-top: 20px;
  letter-spacing: 1px;
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  font-family: 'Comic Sans MS';
}

.homePage {
  height: 500px;
}

.icon2048,
.iconThree,
.iconDemo {
  font-family: Cascadia Code;
  cursor: pointer;
  display: inline-block;
  width: 130px;
  color: white;
  font-size: 40px;
  line-height: 130px;
  border-radius: 20px;
  font-weight: 700;
  transition: all 0.2s;
  margin-right: 20px;
}

.icon2048 {
  background-image: linear-gradient(to top, #30c5d0 0%, #d62178 100%);
}

.iconThree {
  font-size: 30px;
  background-image: linear-gradient(45deg, #c73743 0%, #21cad6 100%);
}

.iconDemo {
  background-image: linear-gradient(to right, #a1a14e 0%, #ed6fe2 100%);
}

.icon2048:hover,
.iconThree:hover,
.iconDemo:hover {
  scale: 1.1;
  /* background-image: linear-gradient(to top, #30c5d0 5%, #e64d97 100%); */
  transition: all 0.2s;
}
</style>
