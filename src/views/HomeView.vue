<template>
  <div class="home">
    <nav>
      <div v-for="film in films" v-bind:key="film.id" class="wrap">
        <router-link
          :to="'/about/' + film.title + '+' + film.year"
        >
          <FilmCard
            :title="film.title"
            :imgSrc="film.imgSrc"
            :year="film.year"
          />
        </router-link>
      </div>
    </nav>
  </div>
</template>

<script>
// @ is an alias to /src
import FilmCard from "@/components/FilmCard.vue";

export default {
  name: "HomeView",
  components: {
    FilmCard,
  },
  data() {
    return {
      films: [
        {
          title: "dsdfs",
          year: "1982",
          imgSrc:
            "https://www.fonstola.ru/pic/201308/1600x900/fonstola.ru_108950.jpg",
        },
      ],
    };
  },
};
</script>
<style>
.home {
  display: flex;
  flex-wrap: wrap;
}
</style>
