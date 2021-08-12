<template>
  <div class="container w-4/5 mx-auto">
    <div class="header w-full h-24 border-b-3 border-primary flex flex-row pt-7">
      <logo/>
      <h1 class="text-primary text-xl font-bold pl-2">Text Editor</h1>

    </div>
    <!--     flex flex-row flex-nowrap-->
    <section id="main" class="min-h-screen grid grid-flow-col grid-cols-5 gap-1 grid-rows-1">
      <div class="bg-gray-300 h-full col-span-4 pt-20 flex flex-row justify-center">
        <!--                <div class="canvas-container w-4/5 ">-->
        <canvas id="canvas" class="mx-auto"></canvas>
        <!--                </div>-->
      </div>
      <div class="h-full bg-primary col-span-1">
        <div class="layer" v-for="(layer, i) in textObjects" v-bind:key="i">
          <h3>Text Layer {{ i }}</h3>
          <label for="content">Enter text</label>
          <input type="text" id="content" name="content" v-model="layer.text">
          <div>
            <label for="size">Font size</label>
            <!--          @change="textbox.set({size: textArray[0].size})-->
            <!--          @change="textbox.size = textArray[0].size"-->
            <!--            @change="changeObject('size', Number(textArray[0].size))"-->
            <input type="text" id="size" name="size" v-model="layer.size"
            >
          </div>
          <div>
            <label for="content">Line Height</label>
            <input type="text" id="lineHeight" name="lineHeight" v-model="textArray[0].lineHeight">
          </div>
          <div>
<!--            <label for="content">Change Font Family-->
              <label for="fonts">Choose a Font Family:</label>
              <select id="fonts" name="fonts">
                <option :value="layer.fontFamily">Volvo</option>
                <option value="saab">Saab</option>
                <option value="fiat">Fiat</option>
                <option value="audi">Audi</option>
              </select>
<!--              <input type="text" id="fontFam" name="fontFam" v-model="textArray[0].fontFam">-->
          </div>
          <div class="bg-blue-500">
            <div>{{ textArray[0].content }}</div>
          </div>
        </div>
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
      fontFamilyArray: ["Inter", "Times New Roman", "Arial", "Georgia", "Roboto", "Verdana", "Tahoma", "Courier", "Tahoma", "Trebuchet"],
      textArray: [
        {
          content: "words words",
          x: "",
          y: "",
          fontFam: "",
          size: "",
          lineHeight: "",
        },
      ],
      textObjects: [],
      textbox: {},
      canvas: {},
    }

  },
  mounted() {
    // const canvas = new fabric.Canvas('canvas', {
    //   width: 500,
    //   height: 500,
    //   backgroundColor: 'white'
    // });
    this.canvas = this.initCanvas('canvas');
    this.canvas.renderAll();

    // canvas.on('mouse:over', (e) => {
    //   console.log(e);
    // })
// 'This is a Textbox object'
    this.textbox = new fabric.Textbox('words', {
      left: 50,
      top: 50,
      fill: '#880E4F',
      stroke: "#D81B60",
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

    console.log(this.canvas.getObjects());


  },
  methods: {
    initCanvas(id) {
      return new fabric.Canvas(id, {
        width: 600,
        height: 600,
        backgroundColor: 'white'
      });
    },
    changeObject(key, value) {
      this.textbox.set({size: value})
      console.log(this.textbox);
      // this.canvas.renderAll();
      this.canvas.requestRenderAll();

    }
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

</style>
