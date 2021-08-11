<template>
  <div class="container w-4/5 mx-auto">
    <div class="header w-full h-24 bg-green-400">
      <h1>Text Editor</h1>
    </div>
    <section id="main flex flex-row flex-nowrap min-h-screen">
      <div class="w-4/5 bg-gray-300 m-0 h-full">
        <!--        <div class="canvas-container h-80 w-80 bg-white">-->
        <canvas id="canvas" class=" mx-auto my-auto"></canvas>
        <!--        </div>-->
      </div>
      <div class="w-1/5 h-full">
        <h3>Text Layer</h3>
        <label for="content">Enter text</label>
        <input type="text" id="content" name="content" v-model="textArray[0].content" @change="changeObject()">
        <div>
          <label for="size">Font size</label>
          <input type="text" id="size" name="size" v-model="textArray[0].size" @change="textbox.set({size: textArray[0].size})">
        </div>
        <div>
          <label for="content">Line Height</label>
          <input type="text" id="lineHeight" name="lineHeight" v-model="textArray[0].lineHeight">
        </div>
        <div>
          <label for="content">Change Font Family</label>
          <input type="text" id="fontFam" name="fontFam" v-model="textArray[0].fontFam">
        </div>
      </div>
    </section>
    <div class="bg-blue-500">
      <p>{{ textArray[0].content }}</p>
    </div>
  </div>
</template>

<script>
import {fabric} from 'fabric'

export default {
  name: 'TextEditor',
  props: {},
  data() {
    return {
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
      textbox: {}
    }

  },
  mounted() {
    // const canvas = new fabric.Canvas('canvas', {
    //   width: 500,
    //   height: 500,
    //   backgroundColor: 'white'
    // });
    const canvas = this.initCanvas('canvas');
    canvas.renderAll();

    // canvas.on('mouse:over', (e) => {
    //   console.log(e);
    // })
// 'This is a Textbox object'
    this.textbox = new fabric.Textbox( this.textArray[0].content , {
      left: 50,
      top: 50,
      fill: '#880E4F',
      stroke: "#D81B60",
      strokeWidth: 2,
      size: 16,
      fontFamily: "Roboto",
      lineHeight: 0.5,
    });

    canvas.add(this.textbox);

    console.log(this.textbox);

  },
  methods: {
    initCanvas(id) {
      return new fabric.Canvas(id, {
        width: 500,
        height: 500,
        backgroundColor: 'white'
      });
    },
    changeObject() {
      // canvas.renderAll();
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
