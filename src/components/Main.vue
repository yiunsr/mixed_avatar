<template>
  <div id="main" class="fill-height mt-2 mx-4">
    <v-row>
      <v-col cols="2">
        <div id="avataaars" refs="mix_avatar">
          <v-sheet position="fixed">
            <avataaars
              :topType="avatarValue['topType']"
              :eyebrowType="avatarValue['eyebrowType']"
              :eyeType="avatarValue['eyeType']"
              :facialHairType="avatarValue['facialHairType']"
              :mouthType="avatarValue['mouthType']"
              :clotheType="avatarValue['clotheType']"
              :graphicShirtType="avatarValue['graphicShirtType']"
              :accessoriesType="avatarValue['accessoryType']"
              :hairColor="avatarValue['hairColor']"
              :skinColor="avatarValue['skinColor']"
            >
            </avataaars>
            <v-btn @click="download('svg')">SVG Download</v-btn>
          </v-sheet>
        </div>
      </v-col>
      <v-col cols="10">
        <div id="part-box-wrap">
          <v-expansion-panels>
            <v-expansion-panel v-for="(item) in [
              {desc: 'skin color', name: 'skinColor', 
                type: 'color', swatches: skinColorsSwatches },
              {desc: 'top & hair', name: 'topType', names: 'topTypes'},
              {desc: 'top & hair color', name: 'hairColor', names: 'hairColors', 
                type: 'color', swatches: hairColorSwatches },
              {desc: 'eyebrow', name: 'eyebrowType', names: 'eyebrowTypes'},
              {desc: 'eye', name: 'eyeType', names: 'eyeTypes'},
              {desc: 'mouth', name: 'mouthType', names: 'mouthTypes'},
              {desc: 'facial Hair', name: 'facialHairType', names: 'facialHairTypes'},
              {desc: 'accessories', name: 'accessoryType', names: 'accessoriesTypes'},
              {desc: 'clothes', name: 'clotheType', names: 'clothesType'},
              {desc: 'graphic shirt', name: 'graphicShirtType', names: 'GraphicShirtTypes'},
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
  import { hairColors, hairColorSwatches, skinColors, skinColorsSwatches, hatAndShirtColors } from '@/assetsTypes/colors'
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
      let hatAndShirtColor = this.getRandomChoice(Object.keys(hatAndShirtColors));
      let avatarType = {
        topTypes, eyebrowTypes, eyeTypes, mouthTypes, clothesType,
        accessoriesTypes, facialHairTypes, GraphicShirtTypes,
         hatAndShirtColors,
      }
      let avatarValue = {
        topType, eyebrowType, eyeType, mouthType, clotheType,
        accessoryType, facialHairType, graphicShirtType, 
        hairColor, skinColor, hatAndShirtColor,
      };
      return {
        hairColorSwatches, skinColorsSwatches,
        avatarType, avatarValue,
      }
    },
    methods: {
      getRandomChoice (items) {
          const itemsLength = Object.entries(items).length
          return Object.entries(items)[Math.floor((Math.random()*(itemsLength)))][1]
      },
      download(file_type){
        if(file_type=="svg"){
          let svgEl = document.querySelector("#avataaars svg");
          svgEl.setAttribute("xmlns", "http://www.w3.org/2000/svg");
          var svgData = svgEl.outerHTML;
          var preface = '<?xml version="1.0" standalone="no"?>\r\n';
          var svgBlob = new Blob([preface, svgData], {type:"image/svg+xml;charset=utf-8"});
          var svgUrl = URL.createObjectURL(svgBlob);
          var downloadLink = document.createElement("a");
          downloadLink.href = svgUrl;
          downloadLink.download = "avatar.svg";
          document.body.appendChild(downloadLink);
          downloadLink.click();
          document.body.removeChild(downloadLink);
        }
      }
    },
  }
</script>

<style scoped>
#main{
  height: calc(100vh - 100px);
}
#avataaars{
  margin-left: 8px;
  width: 180px;
}
.item{
  width: 110px;
  margin-top: 8px;
}
</style>
