<template>
  <p>Hola</p>
  <div class="display">
    <img :src="url" alt="A dog" class="main-img" />
    <button @click="Next" class="next">></button>
  </div>
  <button @click="Like">Like</button>
  <div class="dogs-container">
    <span v-for="(dog, index) in likedDogs" :key="dog" class="dogCard">
      <img :src="dog.imgSrc" class="liked-img" />
      <button @click="Dislike(index)">🗑</button>
    </span>
  </div>
</template>
Place the like button on the right-bottom of the image Change the arrow style
and add arrow press functionality Give more style to the liked dogs Research
about a share img option
<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      arrow: "<",
      url: "",
      likedDogs: [],
    };
  },
  created() {
    axios.get("https://dog.ceo/api/breeds/image/random").then((result) => {
      this.url = result.data.message;
    });
  },
  methods: {
    Next() {
      axios.get("https://dog.ceo/api/breeds/image/random").then((result) => {
        this.url = result.data.message;
      });
    },
    Like() {
      this.likedDogs.push({
        imgSrc: this.url,
        breed: "Dog",
      });
      this.Next();
    },
    Dislike(index) {
      this.likedDogs.splice(index, 1);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.display {
  display: flex;
  justify-content: center;
  align-items: center;
}
.main-img {
  width: 500px;
  height: 400px;
}
.next {
  margin-left: -25px;
}
.liked-img {
  width: 105px;
  height: 90px;
  margin: 10px;
}
.dogs-container {
  height: 175px;
  margin-top: 60px;
  display: flex;
  overflow-x: auto;
}
.dogCard {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  height: 135px;
  width: 105px;
  margin: 0px 10px;
}
</style>
