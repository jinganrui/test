<template>
  <div class="home" id="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div v-if="msg">
      name:<input type="file" multiple="multiple" key="name" @change="fnImgSrc" />
    </div>
    <div v-else>
      email:<input type="file" key="email" />
    </div>
    <img v-for="(item, index) of imgs" :key="index" :src="item.imgSrc" alt="" />
    <div>
      {{ oform.name }}
    </div>
    <div>
      {{ oform.email }}
    </div>
    <button @click="iptSwitch">test</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue"

export default {
  name: "home",
  data: () => {
    return {
      imgs: [],
      msg: true,
      oform: {}
    };
  },
  methods: {
    iptSwitch: function() {
      this.msg = !this.msg;
    },
    fnImgSrc: function(e) {
      this.imgs=[];
      var files = e.target.files;
      console.log(files);
      if (files > 0) {
        return;
      }
      for (let i = 0; i < files.length; i++) {
        let reader = new FileReader();
        reader.readAsDataURL(files[i]); // 读出 base64
        reader.onloadend = () => {
          console.log(this.imgs);
          // 图片的 base64 格式, 可以直接当成 img 的 src 属性值
          this.imgs.push({ imgSrc: `${reader.result}` });
        };
      }
    }
  },
  computed: {},
  components: {
    HelloWorld
  }
};
</script>
<style scoped>
  img{
    max-width: 300px;
    height: auto;
    margin: 0 auto;
  }
</style>
