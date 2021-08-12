<template>
  <div class="header w-full h-24 border-b-3 flex flex-row pt-5 bg-white">
    <div class="container w-4/5 mx-auto flex flex-row">
      <logo/>
      <h1 class="text-primary text-xl font-bold pl-2">Text Editor</h1>
    </div>
  </div>
  <div class="container w-4/5 mx-auto">
    <section id="main" class="min-h-screen grid grid-flow-col grid-cols-5 gap-0 grid-rows-1 rounded-lg">
      <div class="bg-gray-300 h-full col-span-4 pt-20 flex flex-row justify-center">
        <canvas id="canvas" class="mx-auto"></canvas>
      </div>
      <div class="h-full bg-green-400 col-span-1  p-4">
        <button
            class="w-full h-10 text-center bg-white rounded-sm font-bold text-green-400 hover:bg-green-50 transition ease-in-out duration-500"
            @click="addNewLayer()">New Text Layer
        </button>
        <form class="divide-y divide-light-green-400">
          <div class="layer pt-2 pb-4">
            <h3 class="font-bold text-lg">Text Layer</h3>
            <label for="content">Enter text</label>
            <input class="bg-gray-100 px-2 h-8 rounded-md" type="text" id="content" name="content"
                   v-model="currentSelection.text">
            <div>
              <label for="size">Font size</label>
              <input class="bg-gray-100 px-2 h-8 rounded-md" type="text" id="size" name="size"
                     v-model="currentSelection.fontSize">
            </div>
            <div>
              <label for="content">Line Height</label>
              <input class="bg-gray-100 px-2 h-8 rounded-md" type="text" id="lineHeight" name="lineHeight"
                     v-model="currentSelection.lineHeight">
            </div>
            <div>
              <label for="fonts">Choose Font Family:</label>
              <select class="bg-gray-100 px-2 h-8 rounded-md" id="fonts" name="fonts"
                      v-model="currentSelection.fontFamily">
                <option v-for="(font, i) in fontFamilyArray" :value="font" :key="i">{{ font }}</option>
              </select>
            </div>
          </div>
        </form>
      </div>
    </section>
  </div>
</template>

<script>
import logo from "./partials/logo"
import {fabric} from 'fabric'

export default {
  name: 'TextEditor',
  components: {
    logo
  },
  props: {},
  data() {
    return {
      currentSelection: {
        text: "",
        size: "",
        fontFamily: "",
        lineHeight: "",
      },
      fontFamilyArray: ["Inter", "Times New Roman", "Arial", "Georgia", "Roboto", "Verdana", "Tahoma", "Courier", "Tahoma", "Trebuchet"],
      textObjects: [],
      canvas: {},
    }

  },
  mounted() {
    this.canvas = this.initCanvas('canvas');
    this.canvas.renderAll();

    this.textbox = new fabric.Textbox('words', {
      left: 50,
      top: 50,
      fill: '#a71f67',
      stroke: "#cb0c51",
      strokeWidth: 2,
      size: 16,
      fontFamily: "Roboto",
      lineHeight: 0.5,
    });

    this.textbox2 = new fabric.Textbox('more words', {
      left: 50,
      top: 50,
      fill: '#2a6547',
      stroke: "#50bf87",
      strokeWidth: 2,
      size: 16,
      fontFamily: "Roboto",
      lineHeight: 0.5,
    });

    this.canvas.add(this.textbox, this.textbox2);
    this.textObjects = this.canvas.getObjects();

    this.canvas.on('selection:created', (event) => {
      console.log(event.target);
      this.currentSelection = event.target;
    })

    this.canvas.on('selection:updated', (event) => {
      this.currentSelection = event.target;
    })

    this.canvas.on('selection:cleared', () => {
      this.currentSelection = {
        text: "",
        size: "",
        fontFamily: "",
        lineHeight: "",
      };
    })

    this.canvas.on({'object:scaling': (event) => {
        var f = Math.round(event.target.fontSize * event.target.scaleX * 10) / 10;
        var l = Math.round( event.target.lineHeight * event.target.scaleY * 10) / 10;

    event.target.set({
        'fontSize'     : f,
        'lineHeight'      : l,
        'scaleX'     : 1,
        'scaleY'     : 1
    });
}
});

  },
  methods: {
    initCanvas(id) {
      return new fabric.Canvas(id, {
        width: 600,
        height: 600,
        backgroundColor: 'white'
      });
    },
    addNewLayer() {
      this.canvas.add(new fabric.Textbox('write here', {
            left: 50,
            top: 50,
            fill: '#0a1710',
            stroke: "#3d3e3e",
            strokeWidth: 2,
            size: 16,
            fontFamily: "Roboto",
            lineHeight: 1,
          })
      );
      console.log(this.canvas.getObjects());
    },
  },
}
</script>

<style scoped>
h1 {
  line-height: 70px;
  font-family: 'Inter';
}

#canvas {
  margin: 0 auto;
}

label {
  display: block;
}
</style>
