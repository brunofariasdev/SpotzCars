<template>
  <div>
    <div id="img" :class="className" :style="bgImgStyle"></div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      images: [
        "https://unsplash.com/photos/ZRns2R5azu0/download?w=2400",
        "https://unsplash.com/photos/FMbWFDiVRPs/download?w=2400",
        "https://unsplash.com/photos/m3m-lnR90uM/download?w=2400",
      ],
      atualImg: 0,
      className: "fade",
      opacity: 0,
    };
  },
  mounted() {
    setInterval(() => {
      let getAtual = this.atualImg;

      let totalImg = this.images.length;
      if (this.atualImg < totalImg - 1) {
        ++getAtual;
        this.changeImg(getAtual);
      } else {
        this.changeImg(0);
      }
    }, 7000);

    /**
     * preload img
     */
    this.images.forEach((str) => {
      const img = document.createElement("img");
      img.src = str;
      img.hidden = true;
      img.onload = () => {
        img.remove();
      };
    });
  },
  computed: {
    bgImgStyle() {
      return {
        "background-image": `url(${this.images[this.atualImg]})`,
        opacity: this.opacity,
      };
    },
  },
  methods: {
    // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
    changeImg(atual) {
      this.atualImg = atual;
      this.className = "fade";
      this.opacity = 0.3;
      this.upOpactiy();
      console.log("img", this.atualImg);
      setTimeout(() => {
        this.downOpactiy();
      }, 4000);
      return;
    },
    upOpactiy() {
      if (this.opacity < 1) {
        this.opacity += 0.07;
        console.log("up", this.opacity);
        setTimeout(() => {
          this.upOpactiy();
        }, 100);
      } else {
        this.opacity = 1;
      }
    },
    downOpactiy() {
      if (this.opacity > 0.3) {
        this.opacity -= 0.07;
        console.log("down", this.opacity);
        setTimeout(() => {
          this.downOpactiy();
        }, 100);
      } else {
        this.opacity = 0.2;
      }
    },
  },
};
</script>
<style>
#img {
  width: 95vw;
  height: 95vh;
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
