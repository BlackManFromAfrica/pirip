<template lang="">
  <div class="w-full">
    <v-text-field
      clearable
      v-model.trim="title"
      label="Название"
      required
      color="success"
      class="w-1/5 text-black mt-5 ml-4"
    ></v-text-field>
    <v-container fluid>
      <v-textarea
        clearable
        class="text-black"
        color="success"
        clear-icon="mdi-close-circle"
        label="Описание"
        v-model.trim="description"
      ></v-textarea>
    </v-container>
    <v-carousel
      hide-delimiters
      show-arrows="hover"
      height="400px"
      progress="secondary"
      color="success"
    >
      <div class="h-full flex justify-center items-center">
        <h1 v-if="list.length === 0" class="text-blue flex flex-col w-fit">
          Выберите место
          <svg
            width="40"
            height="40"
            class="mx-auto animate__animated animate__fadeInDown animate__infinite"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M19.92 8.95001L13.4 15.47C12.63 16.24 11.37 16.24 10.6 15.47L4.08002 8.95001"
              stroke="white"
              stroke-width="1.5"
              stroke-miterlimit="10"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </h1>
        <h1
          v-else
          class="mt-[-35px] absolute text-slate-400 animate__animated animate__fadeOut animate__slower animate__infinite"
        >
          листайте
        </h1>
      </div>

      <v-carousel-item v-for="(item, i) in list" :key="i">
        <div
          class="relative flex items-center w-full h-full justify-around p-6"
        >
          <div class="relative flex justify-center items-center">
            <img :src="item.src" alt="" />

            <v-dialog v-model="dialog">
              <template v-slot:activator="{ props }">
                <svg
                  class="absolute opacity-30 hover:opacity-70 cursor-pointer duration-200"
                  v-bind="props"
                  width="200"
                  height="200"
                  viewBox="0 0 24 24"
                  fill="none"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    d="M9 10C10.1046 10 11 9.10457 11 8C11 6.89543 10.1046 6 9 6C7.89543 6 7 6.89543 7 8C7 9.10457 7.89543 10 9 10Z"
                    stroke="white"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                  <path
                    d="M13 2H9C4 2 2 4 2 9V15C2 20 4 22 9 22H15C20 22 22 20 22 15V10"
                    stroke="white"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                  <path
                    d="M15.75 5H21.25"
                    stroke="white"
                    stroke-width="1.5"
                    stroke-linecap="round"
                  />
                  <path
                    d="M18.5 7.75V2.25"
                    stroke="white"
                    stroke-width="1.5"
                    stroke-linecap="round"
                  />
                  <path
                    d="M2.67004 18.95L7.60004 15.64C8.39004 15.11 9.53004 15.17 10.24 15.78L10.57 16.07C11.35 16.74 12.61 16.74 13.39 16.07L17.55 12.5C18.33 11.83 19.59 11.83 20.37 12.5L22 13.9"
                    stroke="white"
                    stroke-width="1.5"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                  />
                </svg>
              </template>

              <v-card class="w-1/4 mx-auto">
                <v-text-field
                  clearable
                  hide-details="auto"
                  label="Ссылка"
                ></v-text-field>
              </v-card>
            </v-dialog>
          </div>

          <div class="w-3/5 flex flex-col items-center self-center">
            <v-container>
              <v-textarea
                clearable
                background-color="grey lighten-2"
                color="cyan"
                :label="item.name"
                class="text-white"
                :model-value="item.description"
              ></v-textarea>
            </v-container>
          </div></div
      ></v-carousel-item>
    </v-carousel>
    <div class="w-full flex justify-around h-1/2">
      <v-list theme="none" class="mx-auto">
        <v-list-group value="Places">
          <template v-slot:activator="{ props }">
            <v-list-item v-bind="props"
              ><span class="text-[#bfe2ff]">Выберите место</span></v-list-item
            >
          </template>

          <v-list-group value="Culture">
            <template v-slot:activator="{ props }">
              <v-list-item
                v-bind="props"
                active-color="rgb(236,72,153)"
                class="hover:text-white"
              >
                Места культуры и отдыха</v-list-item
              >
            </template>

            <v-list-item
              active-color="purple"
              v-for="([title, description, src, coordinates], i) in Culture"
              :key="i"
              :title="title"
              :value="title"
              class="hover:text-white"
              v-on:click="choice(title, description, src, coordinates, i)"
            ></v-list-item>
          </v-list-group>

          <v-list-group value="Monuments">
            <template v-slot:activator="{ props }">
              <v-list-item
                v-bind="props"
                title="Памятники и скульптуры"
              ></v-list-item>
            </template>

            <v-list-item
              v-for="([title, icon], i) in Monuments"
              :key="i"
              :value="title"
              :title="title"
              :prepend-icon="icon"
            ></v-list-item>
          </v-list-group>
        </v-list-group>
      </v-list>
      <draggable
        :list="list"
        :disabled="!enabled"
        item-key="name"
        class="list-group my-auto max-w-2xl"
        ghost-class="ghost"
        :move="checkMove"
        :onChange="handleChange"
        @start="dragging = true"
        @end="dragging = false"
      >
        <template #item="{ element, index }">
          <div>
            <v-btn
              variant="outlined"
              color="secondary"
              class="list-group-item mx-2"
              :class="{ 'not-draggable': !enabled }"
            >
              {{ element.name }}
            </v-btn>
            <v-btn @click="removeAt(index)" variant="text" color="secondary"
              ><v-icon>mdi-delete</v-icon></v-btn
            >
          </div>
        </template>
      </draggable>
    </div>
  </div>
  <!-- <div
      class="mix-blend-soft-light"
      id="map"
      style="width: 100%; height: 400px"
    ></div> -->
  <div
    v-if="list.length === 0"
    class="flex items-center justify-center h-[400px] w-full"
  >
    <h1
      class="w-fit text-slate-400 animate__animated animate__fadeOut animate__slower animate__infinite"
    >
      Здесь появится карта
    </h1>
  </div>
  <mapVue :key="renderMapCount" v-else></mapVue>
  <v-btn @click="publish" class="w-full" variant="outlined" color="success">
    Опубликовать
  </v-btn>
</template>
<script>
import draggable from "vuedraggable";
import mapVue from "@/components/map.vue";
import { toRaw } from "vue";
export default {
  name: "simple",
  display: "Simple",
  order: 1,
  components: {
    draggable,
    mapVue,
  },

  data: () => ({
    dialog: false,
    title: "",
    description: "",
    list: [],
    route: [],
    renderMapCount: 0,
    open: ["Places"],
    Culture: [
      [
        "Русский драматический театр",
        "Здание русского драматического театра (бывшее здание Дворца культуры «Машиностроитель») яркий пример развития советской архитектуры конструктивизма к архитектуре 50-х годов.",
        "https://www.izh.ru/res_ru/0_image_16378_1.jpg",
        [56.84127582532452, 53.205406197923615],
      ],
      [
        "Государственный национальный театр Удмуртской Республики",
        "Предшественником Государственного национального театра был Центральный удмуртский клуб «Красный удмурт», возникший в 1923 году. При нём действовал драматический кружок, давший начало самодеятельному театру, на базе которого 7 февраля 1931 года был создан первый профессиональный удмуртский театр.",
        "https://www.izh.ru/res_ru/0_image_16379_1.jpg",
        [56.87176889746844, 53.24509912866931],
      ],
      [
        "Государственный цирк Удмуртской Республики",
        "Первый в Ижевске цирк открылся в 1895 году на Базарной площади возле мучного базара (пересечение улиц Горького и Бородина на месте старого корпуса механического института). Постоянно действующее деревянное здание было построено на средства предпринимателя А. Г. Коромыслова. В цирке гастролировали артисты из Вены, Парижа, Берлина, проводились чемпионаты борцов. Цирк сгорел во время Гражданской войны.",
        "https://www.izh.ru/res_ru/0_image_16377_1.jpg",
        [56.84133, 53.210987],
      ],
      [
        "Государственный театр кукол Удмуртской Республики",
        "Современное здание государственного театра кукол построено в 1980 году, однако история театра кукол в Ижевске началась намного раньше - в 1935 году. Его организаторами стали С. Ломовская и М. Точилина (Стрелкова), окончившие специальные курсы кукловодов при Центральном театре кукол под руководством С.Образцова.",
        "https://www.izh.ru/res_ru/0_image_16374_1.jpg",
        [56.848675, 53.222782],
      ],
    ],
    Monuments: [
      ["Create", "mdi-plus-outline"],
      ["Read", "mdi-file-outline"],
      ["Update", "mdi-update"],
      ["Delete", "mdi-delete"],
    ],
    enabled: true,
    dragging: false,
  }),
  computed: {
    draggingInfo() {
      return this.dragging ? "under drag" : "";
    },
  },
  methods: {
    renderMap: function () {
      ymaps.ready(init);
      let points = toRaw(this.route);
      function init() {
        // Creating the map.
        var myMap = new ymaps.Map("map", {
          // The map center coordinates.
          // Default order: “latitude, longitude”.
          // To not manually determine the map center coordinates,
          // use the Coordinate detection tool.
          center: [56.852946, 53.208719],
          // Zoom level. Acceptable values:
          // from 0 (the entire world) to 19.
          zoom: 14,
        });
        var multiRoute = new ymaps.multiRouter.MultiRoute(
          {
            referencePoints: points,
            params: {
              // Тип маршрута: на общественном транспорте.
              routingMode: "pedestrian",
            },
          },
          {
            // Автоматически устанавливать границы карты так,
            // чтобы маршрут был виден целиком.
            boundsAutoApply: true,
          }
        );

        myMap.geoObjects.add(multiRoute);
      }
      this.renderMapCount++;
    },
    handleChange: function () {
      toRaw(this.list).map((e, count) => {
        this.route[count] = e.coordinates;
      });
      this.renderMap();
    },
    removeAt(idx) {
      this.list.splice(idx, 1);
      this.route.splice(idx, 1);
      this.renderMap();
    },
    choice: function (title, description, src, coordinates, i) {
      this.list.push({
        name: `${title}`,
        description: `${description}`,
        src: `${src}`,
        coordinates: coordinates,
      });
      this.route.push(toRaw(coordinates));
      this.renderMap();
    },
    publish: function () {
      // try {
      //   await axios.post("/polls", this.data);
      // } catch (error) {
      //   console.warn(error);
      //   alert("Ошибка при создании опроса");
      // }
      console.log(this.data);
    },
  },
};
</script>
<style></style>
