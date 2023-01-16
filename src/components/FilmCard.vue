<template lang="">
  <div class="card">
    <div class="card-front">
      <img :src="imgSrc" alt="" />
    </div>
    <div class="card-back">
      <h2>
        {{ title }}<br />
        <span>{{ year }}</span>
      </h2>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    title: String,
    year: String,
    imgSrc: String,
  },
};
</script>
<style scoped>
.card {
  height: 400px;
  width: 300px;
  transform-style: preserve-3d;
  perspective: 600px;
  transition: 0.5s;
}
img {
  width: 100%;
  height: 100%;
}
.card:hover .card-front {
  transform: rotateX(-180deg);
}
.card:hover .card-back {
  transform: rotateX(0deg);
}

.card-front {
  height: 100%;
  width: 100%;
  transform: rotateX(0deg);
  transition: 0.5s;
}

.card-back {
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-color: #000000;
  backface-visibility: hidden;
  transform: rotateX(180deg);
  transition: 0.5s;
  color: #ffffff;
  text-align: center;
}
.card-back h2 {
  margin: 60% auto 35% auto;
  font-size: 26px;
}
.card-back h2 span {
  font-size: 20px;
}
.card-back a {
  height: 20px;
  width: 20px;
  padding: 5px 5px;
  border-radius: 4px;
  line-height: 20px;
}
.card-back a:hover {
  color: #000000;
  background-color: #fff;
}
</style>
