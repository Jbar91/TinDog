<template>
  <section class="main-app">
    <h1>Choose a Cute Partner</h1>
    <section class="main-display">
      <div class="main-container">
        <img :src="img" alt="A dog" class="main-img" />
        <span>
          <button
            @click="Like"
            v-if="!hover"
            @mouseenter="ChangeColor"
            class="btns "
          >
            <img src="../assets/Imgs/Heart.svg" alt="" />
          </button>
          <button
            @click="Like"
            v-if="hover"
            @mouseleave="ChangeColor"
            class="btns"
          >
            <img src="../assets/Imgs/HeartRed.svg" alt="" class="red-heart" />
          </button>
          <button @click="Next" class="btns ">
            <img src="../assets/Imgs/RightArrow.svg" alt="" />
          </button>
        </span>
      </div>
    </section>
    <div class="dogs-container">
      <span v-for="(dog, index) in likedDogs" :key="dog" class="dogCard">
        <img :src="dog.imgSrc" class="liked-img" />
        <img
          src="../assets/Imgs/HeartRed.svg"
          @click="Dislike(index)"
          class="liked-dog-btn"
        />
      </span>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      url: "https://dog.ceo/api/breeds/image/random",
      img: "",
      hover: false,
      likedDogs: [],
      heart1: "img/RightArrow.67285f1c.svg",
    };
  },
  created() {
    axios.get(this.url).then((result) => {
      this.img = result.data.message;
    });
  },
  methods: {
    Next() {
      axios.get(this.url).then((result) => {
        this.img = result.data.message;
      });
    },
    Like() {
      this.likedDogs.push({
        imgSrc: this.img,
        breed: "Dog",
      });
      this.Next();
    },
    Dislike(index) {
      this.likedDogs.splice(index, 1);
    },
    ChangeColor() {
      this.hover = !this.hover;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main-app {
  margin: auto;
  background-color: ivory;
  width: 720px;
}
.main-display {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.main-container {
  width: 500px;
  height: 450px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: flex-end;
}
.main-img {
  width: 500px;
  height: 400px;
}
.btns {
  cursor: pointer;
  background-color: ivory;
  margin-left: 10px;
  height: 30px;
  width: 30px;
  padding: 0;
  border: none;
}
.red-heart {
  height: 29px;
  width: 29px;
  padding: 0;
}
.right-arrow {
  background-image: url("../assets/Imgs/RightArrow.svg");
}
.like-btn {
  background-image: url("../assets/Imgs/Heart.svg");
}

.liked-img {
  width: 105px;
  height: 130px;
  margin-bottom: 10px;
}
.dogs-container {
  height: 190px;
  margin-left: 25px;
  margin-top: 30px;
  display: flex;
  overflow-x: auto;
  overflow-y: hidden;
}
.dogCard {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  height: 175px;
  width: 105px;
  margin: 0px 10px;
}
.liked-dog-btn {
  height: 20px;
  width: 20px;
}

::-webkit-scrollbar {
  width: 5px;
  height: 14px;
}

::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey;
  border-radius: 5px;
}

::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: #666;
}
</style>
