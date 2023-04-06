<template>
  <div class="wrapper container flex flex-wrap mx-auto">
    <h1
      class="text-4xl font-bold text-slate-600 block w-full text-center mx-4 my-8"
    >
      Tile Configurator
    </h1>
    <div class="wrapper w-full flex flex-row ">
      
      <div class="left mx-auto w-1/2 flex-col">
        <div class="flex justify-between w-full items-center my-6">
          <div class="flex items-center">
            <div class="text-lg font-medium px-4 py-2 text-white bg-slate-400">
              1
            </div>
            <span
              class="uppercase txt-md leading-1 mx-12 items-center justify-center"
            >
              Select type of tile project:
            </span>
          </div>
        </div>
        <div class="flex justify-between w-full items-center my-2">
          <ul class="buttons flex justify-center -mx-2">
            <li v-for="(item, index) in config" :key="index">
              <a
                :class="{ activeBackground: activeTileQuantity === index }"
                class="button text-md font-medium px-10 py-1 m-2 text-white bg-slate-400 hover:bg-slate-800"
                href="#"
                @click="filterList(item.title), (activeTileQuantity = index)"
                >{{ item.title }}</a
              >
            </li>
          </ul>
        </div>
        <div class="flex justify-between w-full items-center my-6">
          <div class="flex items-center">
            <div class="text-lg font-medium px-4 py-2 text-white bg-slate-400">
              2
            </div>
            <span
              class="uppercase txt-md leading-1 mx-12 items-center justify-center"
            >
              Select floor pattern:
            </span>
          </div>
        </div>
        <div class="flex justify-between w-full items-center">
          <ul class="buttons flex justify-center -mx-2">
            <li v-for="(item, index) in filteredTiles" :key="index" class="">
              <a
                :class="{ activeBorder: activeTilePattern === index }"
                class="w-24 h-24 flex m-2 border-2 border-slate-400 hover:border-slate-800 cursor-pointer"
                href="#"
                @click="(activeTilePattern = index, selectedComponent = componentForTile(item.name))"
              >
                <component :is="componentForTile(item.name)" :opacity="1"  />
              </a>
              <span class="w-full flex justify-center text-center">{{
                item.name
              }}</span>
            </li>
          </ul>
        </div>
        <div class="flex justify-between w-full items-center my-6">
          <div class="flex items-center">
            <div class="text-lg font-medium px-4 py-2 text-white bg-slate-400">
              3
            </div>
            <span
              class="uppercase txt-md leading-1 mx-12 items-center justify-center"
            >
              Select tile size:
            </span>
          </div>
        </div>
        <div class="flex justify-between w-full items-center">
          <ul class="flex justify-center -mx-2">
            <li
              v-for="(size, index) in filteredTiles[0].sizes"
              :key="index"
              class=""
            >
              <a
                :class="{ activeBorder: activeTileSize === index }"
                class="w-auto h-auto block text-center m-2 p-2 border-2 border-slate-400 hover:border-slate-800"
                href="#"
                @click="activeTileSize = index"
              >
                <div>{{ size }}</div>
              </a>
            </li>
          </ul>
        </div>
        <div class="flex justify-between w-full items-center my-6">
          <div class="flex items-center">
            <div class="text-lg font-medium px-4 py-2 text-white bg-slate-400">
              4
            </div>
            <span
              class="uppercase txt-md leading-1 mx-12 items-center justify-center"
            >
              Select texture:
            </span>
          </div>
        </div>
        <div class="flex justify-between w-full items-center">
          <ul class="buttons flex justify-center -mx-2">
            <li v-for="(item, index) in filteredTiles[0].textures" :key="index" class="">
              <a
                :class="{ activeBorder: activeTexture === index }"
                class="w-24 h-24 flex m-2 border-2 border-slate-400 hover:border-slate-800 cursor-pointer"
                href="#"
                @click="(activeTexture = index, selectedTexture = item)"
              >
                <img :src="item"/>
                
              </a>
              
            </li>
          </ul>
        </div>
      </div>
      <div class="right mx-auto w-1/2 flex-col">
        <div class="flex justify-between w-full items-center my-6">
          <div class="flex items-center">
            <div class="text-lg font-medium px-4 py-2 text-white bg-slate-400">
              5
            </div>
            <span
              class="uppercase txt-md leading-1 mx-12 items-center justify-center"
            >
              Preview:
            </span>
          </div>
        </div>
        <div class="flex justify-between w-96 items-center my-2 overflow-hidden">
          <component :is="selectedComponent" :opacity="0.3" />
          <img class="absolute w-96 -z-10" :src="this.selectedTexture"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { markRaw } from "vue";

import GridPattern from "./components/patterns/grid.vue";
import DiamondPattern from "./components/patterns/diamond.vue";

export default {
  name: "App",
  components: {
    GridPattern,
    DiamondPattern,
  },
  data() {
    return {
      GridPattern: markRaw(GridPattern),
      DiamondPattern: markRaw(DiamondPattern),
      add: "",
      selectedComponent: null,
      selectedTexture: "",
      activeTileQuantity: "",
      activeTilePattern: "",
      activeTileSize: "",
      activeTexture: null,
      config: [
        {
          title: "One Tile",
          tiles: [
            { name: "Grid", component: GridPattern },
            { name: "Diamond", component: DiamondPattern },
          ],
          sizes: ["24 x 24", "18 x 18", "12 x 12"],
          textures: [
            "https://images.pexels.com/photos/4664463/pexels-photo-4664463.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1", 
            "https://images.pexels.com/photos/129733/pexels-photo-129733.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
            "https://images.pexels.com/photos/11273855/pexels-photo-11273855.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1"
          ],
        },
        {
          title: "Two Tile",
          tiles: [ { name: "Test" },
            { name: "Test" },],
          sizes: ["6 x 24 / 12 x 24"],
          textures: [],

        },
        {
          title: "Multi Tile",
          tiles: [
            { name: "Test" },
            { name: "Test" },
            { name: "Test" },
            
          ],
          sizes: [`18 x 18 / 2 x 18 / 2 x 2`],
          textures: [],

        },
      ],
      filter: "One Tile",
    };
  },
  computed: {
    
    activeClass() {
      return {
        active: this.activeTileQuantity === index,
        active: this.activeTilePattern === index,
        active: this.activeTileSize === index,
        active: this.activeTexture === index
      };
    },
    filteredTiles() {
      if (this.filter === "One Tile") {
        const result = this.config.find((item) => item.title === "One Tile");
        return result.tiles.map((tile) => ({
          ...tile,
          sizes: result.sizes,
          textures: result.textures
        }));
      } else if (this.filter === "Two Tile") {
        const result = this.config.find((item) => item.title === "Two Tile");
        return result.tiles.map((tile) => ({
          ...tile,
          sizes: result.sizes,
          textures: result.textures

        }));
      } else if (this.filter === "Multi Tile") {
        const result = this.config.find((item) => item.title === "Multi Tile");
        return result.tiles.map((tile) => ({
          ...tile,
          sizes: result.sizes,
          textures: result.textures

        }));
      }
      return [];
    },
  },

  methods: {
    filterList(filter) {
      console.log(filter);
      this.filter = filter;
    },    
    componentForTile(tileName) {
      const flatTiles = this.config.flatMap((config) => config.tiles);
      const tile = flatTiles.find((tile) => tile.name === tileName);
      return tile ? tile.component : "";
    },
    logger(item){
      console.log(item)
    }
    // selectComponent(event) {
    //   this.selectedComponent = this.componentForTile(this.selectedTile.name);
    // },
    // selectedTexture(event) {
    //   this.selectedTexture = event
    //   console.log(this.selectTexture)
    // }
  },
};
</script>

<style scoped>
.activeBorder {
  @apply border-slate-800;
}
.activeBackground {
  @apply bg-slate-800;
}
</style>
