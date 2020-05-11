<template>
  <div class="zq-wrap">
    <h2 class="title">{{ getTitle }}</h2>
    <div class="poem">
      <p>
        {{ poem.content }}
      </p>
      <p>
        【{{ poem.title }}】
        <span class="author">{{ poem.author }}</span>
      </p>
    </div>
    <div class="flex">
      <div class="" v-for="item in showData" :key="item.id">
        <p>{{ item.title }}</p>
        <p>{{ item.desc }}</p>
      </div>
    </div>
    <div class="wave"></div>
  </div>
</template>

<script>
const jinrishici = require("jinrishici");
export default {
  components: {},
  data() {
    return {
      titleData: [
        "Something better will happen",
        "To be a better man",
        "Is life always this hard or just when you're a kid?",
        "It is nice to be needed",
        "The future belongs to those who believe in the beauty of their dreams"
      ],
      poem: {
        content: "相逢祗有梦魂间，可奈梦随春漏短，不到江南。",
        title: "浪淘沙·莫上玉楼看",
        author: "韩疁"
      },
      showData: [
        {
          id: 1,
          title: "BLOG",
          desc: "Write Sth Down",
          src: ""
        },
        {
          id: 2,
          title: "Projects",
          desc: "Sth I Coded",
          src: ""
        }
      ]
    };
  },
  computed: {
    getTitle() {
      const order = Math.floor(Math.random() * 5);
      return this.titleData[order];
    }
  },
  watch: {},
  mounted() {
    this.initRhthy();
  },
  methods: {
    initRhthy() {
      jinrishici.load(result => {
        // 自己的处理逻辑
        console.log(result);
        if (result.status !== "success") {
          return;
        }
        this.poem = {
          content: result.data.content,
          title: result.data.origin.title,
          author: result.data.origin.author
        };
      });
    }
  }
};
</script>
<style scoped>
.zq-wrap {
  position: relative;
  height: 100%;
  padding: 10px;
  z-index: 3;
}
.title {
  padding-top: 60px;
}
.poem {
  position: absolute;
  top: 150px;
  writing-mode: vertical-lr; /*从左向右 从右向左是 writing-mode: vertical-rl;*/
  writing-mode: tb-lr;
  direction: ltr;
  letter-spacing: 2px;
}
.poem p {
  line-height: 35px;
}
.author {
  background: #a77f80;
  color: #e2e4e1;
  font-size: 0.8em;
  padding: 5px 3px;
  border-radius: 6px;
  letter-spacing: 1px;
}
.wave {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
.wave:before,
.wave:after {
  content: "";
  position: absolute;
  left: 50%;
  min-width: 300vw;
  min-height: 300vw;
  background-color: #e2e7e1;
  -webkit-animation-name: rotate;
  animation-name: rotate;
  -webkit-animation-iteration-count: infinite;
  animation-iteration-count: infinite;
  -webkit-animation-timing-function: linear;
  animation-timing-function: linear;
  z-index: -1;
}
.wave:before {
  bottom: 27vh;
  border-radius: 45%;
  animation-duration: 10s;
}

.wave:after {
  bottom: 20vh;
  opacity: 0.5;
  border-radius: 47%;
  animation-duration: 10s;
}
*,
::before,
::after {
  box-sizing: border-box;
  border-width: 0;
  border-style: solid;
  border-color: #7d8971;
}
@keyframes rotate {
  0% {
    transform: translate(-50%, 0) rotateZ(0deg);
  }
  50% {
    transform: translate(-50%, -2%) rotateZ(180deg);
  }
  100% {
    transform: translate(-50%, 0%) rotateZ(360deg);
  }
}
</style>
