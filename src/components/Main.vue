<template>
  <div id="main" class="fill-height mt-2 mx-4">
    <v-row class="mb-2">
      <v-col cols="3">
        <div id="avataaars" refs="mix_avatar">
          <v-sheet class="text-center" position="fixed">
            <avataaars
              :topType="avatarValue['topType']"
              :eyebrowType="avatarValue['eyebrowType']"
              :eyeType="avatarValue['eyeType']"
              :facialHairType="avatarValue['facialHairType']"
              :mouthType="avatarValue['mouthType']"
              :clotheType="avatarValue['clotheType']"
              :graphicType="avatarValue['graphicShirtType']"
              :accessoriesType="avatarValue['accessoryType']"
              :hairColor="avatarValue['hairColor']"
              :facialHairColor="avatarValue['facialHairColor']"
              :skinColor="avatarValue['skinColor']"
              :clotheColor="avatarValue['clotheColor']"
            >
            </avataaars>
            <div class="mt-4 mb-2"><v-btn @click="download_svg('svg')">SVG Download</v-btn></div>
            <div><v-btn @click="download_png">Png Download</v-btn></div>
          </v-sheet>
        </div>
      </v-col>
      <v-col cols="9">
        <div id="part-box-wrap">
          <v-expansion-panels>
            <v-expansion-panel v-for="(item) in [
              {desc: 'skin color', name: 'skinColor', 
                type: 'color', swatches: skinColorsSwatches },
              {desc: 'top & hair', name: 'topType', names: 'topTypes'},
              {desc: 'top & hair color', name: 'hairColor',
                type: 'color', swatches: hairColorSwatches },
              {desc: 'eyebrow', name: 'eyebrowType', names: 'eyebrowTypes'},
              {desc: 'eye', name: 'eyeType', names: 'eyeTypes'},
              {desc: 'mouth', name: 'mouthType', names: 'mouthTypes'},
              {desc: 'facial hair', name: 'facialHairType', names: 'facialHairTypes'},
              {desc: 'facial hair color', name: 'facialHairColor',
                type: 'color', swatches: facialHairColorSwatches },
              {desc: 'accessories', name: 'accessoryType', names: 'accessoriesTypes'},
              {desc: 'clothes', name: 'clotheType', names: 'clothesType'},
              {desc: 'graphic shirt', name: 'graphicShirtType', names: 'GraphicShirtTypes'},
              {desc: 'clothe color', name: 'clotheColor', 
                type: 'color', swatches: clotheColorSwatches },
              ]"
              >
              <v-expansion-panel-title>{{  item.desc  }}</v-expansion-panel-title>
              <v-expansion-panel-text>
                <div class="item-box-wrap" v-if="item.type == 'color'">
                  <v-color-picker v-model="avatarValue[item.name]"
                    hide-inputs show-swatches :swatches="item.swatches"
                  ></v-color-picker>
                </div>
                <div class="item-box-wrap" v-else>
                  <v-radio-group  v-model="avatarValue[item.name]" inline >
                    <v-radio class="item-radio" v-for="(svg_inner, item_name, _) in avatarType[item.names]" :value="item_name">
                      <template v-slot:label>
                        <svg class="item" 
                        viewBox='0 0 264 280' version='1.1'
                        xmlns='http://www.w3.org/2000/svg' xmlns:xlink='http://www.w3.org/1999/xlink'
                        v-html="svg_inner"
                        >
                      </svg>
                      </template>
                    </v-radio>
                  </v-radio-group>
                </div>
              </v-expansion-panel-text>
            </v-expansion-panel>
          </v-expansion-panels>
        </div>
      </v-col>
    </v-row>
  </div>
</template>

<script>
  import { mouthTypes } from '@/assetsTypes/mouth'
  import { eyeTypes } from '@/assetsTypes/eyes'
  import { eyebrowTypes } from '@/assetsTypes/eyebrows'
  import { clothesType } from '@/assetsTypes/clothes'
  import { topTypes } from '@/assetsTypes/top'
  import { accessoriesTypes } from '@/assetsTypes/accessories'
  import { facialHairTypes } from '@/assetsTypes/facial-hair'
  import { GraphicShirtTypes } from '@/assetsTypes/graphic-shirt'
  import { hairColors, hairColorSwatches, facialHairColors, facialHairColorSwatches,
    skinColors, skinColorsSwatches, clotheColors, clotheColorSwatches } 
    from '@/assetsTypes/colors'
  import Avataaars from '@/components/Avataaars.vue'

  export default {
    components: {
      Avataaars
    },
    data() {
      let topType = this.getRandomChoice(Object.keys(topTypes));
      let eyebrowType= this.getRandomChoice(Object.keys(eyebrowTypes));
      let eyeType = this.getRandomChoice(Object.keys(eyeTypes));
      let mouthType = this.getRandomChoice(Object.keys(mouthTypes));
      let accessoryType = this.getRandomChoice(Object.keys(accessoriesTypes));
      let facialHairType = this.getRandomChoice(Object.keys(facialHairTypes));
      let clotheType = this.getRandomChoice(Object.keys(clothesType));
      let graphicShirtType = this.getRandomChoice(Object.keys(GraphicShirtTypes));

      let skinColor = skinColors[this.getRandomChoice(Object.keys(skinColors))];
      let hairColor = hairColors[this.getRandomChoice(Object.keys(hairColors))]; 
      let facialHairColor = facialHairColors[this.getRandomChoice(Object.keys(facialHairColors))];
      let clotheColor = clotheColors[this.getRandomChoice(Object.keys(clotheColors))];
      let avatarType = {
        topTypes, eyebrowTypes, eyeTypes, mouthTypes, clothesType,
        accessoriesTypes, facialHairTypes, GraphicShirtTypes,
        clotheColors,
      }
      let avatarValue = {
        topType, eyebrowType, eyeType, mouthType, clotheType,
        accessoryType, facialHairType, graphicShirtType, 
        hairColor, facialHairColor, skinColor, clotheColor,
      };
      return {
        hairColorSwatches, facialHairColorSwatches, skinColorsSwatches, clotheColorSwatches,
        avatarType, avatarValue,
      }
    },
    methods: {
      getRandomChoice (items) {
          const itemsLength = Object.entries(items).length
          return Object.entries(items)[Math.floor((Math.random()*(itemsLength)))][1]
      },
      download_svg(file_type){
        let svgEl = document.querySelector("#avataaars svg");
        svgEl.setAttribute("xmlns", "http://www.w3.org/2000/svg");
        let svgData = svgEl.outerHTML;
        let preface = '<?xml version="1.0" standalone="no"?>\r\n';
        let svgBlob = new Blob([preface, svgData], {type:"image/svg+xml;charset=utf-8"});
        let svgUrl = URL.createObjectURL(svgBlob);
        let downloadLink = document.createElement("a");
        downloadLink.href = svgUrl;
        downloadLink.download = "avatar.svg";
        document.body.appendChild(downloadLink);
        downloadLink.click();
        document.body.removeChild(downloadLink);
      },
      // https://stackoverflow.com/a/37236038/6652082
      download_png(){
        let svgEl = document.querySelector("#avataaars svg");
        svgEl.setAttribute("xmlns", "http://www.w3.org/2000/svg");
        let svgData = svgEl.outerHTML;
        let preface = '<?xml version="1.0" standalone="no"?>\r\n';
        let svgBlob = new Blob([preface, svgData], {type:"image/svg+xml;charset=utf-8"});
        let svgUrl = URL.createObjectURL(svgBlob);

        let canvas = document.createElement("canvas");
        let w=264;
        let h=280;

        canvas.width = w;
        canvas.height = h;

        let ctx = canvas.getContext("2d");

        let img = new Image();
        img.onload = function() {
          ctx.drawImage(img, 0, 0);
          let imgURL = canvas.toDataURL("image/png");
          URL.revokeObjectURL(imgURL);
          let dlLink = document.createElement('a');
          dlLink.download = "image";
          dlLink.href = imgURL;
          dlLink.dataset.downloadurl = ["image/png", dlLink.download, dlLink.href]
                                      .join(':');
          document.body.appendChild(dlLink);
          dlLink.click();
          document.body.removeChild(dlLink);
        }
      img.src = svgUrl;
      },
    },
  }
</script>

<style scoped>
#main{
  height: calc(100vh - 100px);
}
#avataaars{
  margin-left: 8px;
  width: 400px;
}
#avataaars svg{
  width: 360px;
}
.item{
  width: 110px;
  margin-top: 8px;
}
#part-box-wrap{
  --avataaar-hair-color: black;
}
</style>
