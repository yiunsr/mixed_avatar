<template>
    <svg
        viewBox='0 0 264 280'
        version='1.1'
        xmlns='http://www.w3.org/2000/svg'
        xmlns:xlink='http://www.w3.org/1999/xlink'>
        <desc>Created with getavataaars.com</desc>
        <defs>
          <circle id='path-1' cx='120' cy='120' r='120'></circle>
          <path
            d='M12,160 C12,226.27417 65.72583,280 132,280 C198.27417,280 252,226.27417 252,160 L264,160 L264,-1.42108547e-14 L-3.19744231e-14,-1.42108547e-14 L-3.19744231e-14,160 L12,160 Z'
            id='path-2'></path>
          <path
            d='M124,144.610951 L124,163 L128,163 L128,163 C167.764502,163 200,195.235498 200,235 L200,244 L0,244 L0,235 C-4.86974701e-15,195.235498 32.235498,163 72,163 L72,163 L76,163 L76,144.610951 C58.7626345,136.422372 46.3722246,119.687011 44.3051388,99.8812385 C38.4803105,99.0577866 34,94.0521096 34,88 L34,74 C34,68.0540074 38.3245733,63.1180731 44,62.1659169 L44,56 L44,56 C44,25.072054 69.072054,5.68137151e-15 100,0 L100,0 L100,0 C130.927946,-5.68137151e-15 156,25.072054 156,56 L156,62.1659169 C161.675427,63.1180731 166,68.0540074 166,74 L166,88 C166,94.0521096 161.51969,99.0577866 155.694861,99.8812385 C153.627775,119.687011 141.237365,136.422372 124,144.610951 Z'
            id='path-silhouette'></path>
          <linearGradient id="color-hair">
            <stop :stop-color="hairColor"/>
          </linearGradient>
          <linearGradient id="color-facial-hair">
            <stop :stop-color="facialHairColor"/>
          </linearGradient>
          <linearGradient id="color-hat">
            <stop :stop-color="hairColor"/>
          </linearGradient>
          <linearGradient id="color-shirt">
            <stop :stop-color="clotheColor"/>
          </linearGradient>
        </defs>
        <g
          id='Avataaar'
          stroke='none'
          stroke-width='1'
          fill='none'
          fill-rule='evenodd'>
          <g
            transform='translate(-825.000000, -1100.000000)'
            id='Avataaar/Circle'>
            <g transform='translate(825.000000, 1100.000000)'>
            <template v-if="isCircle">
                <g
                  id='Circle'
                  stroke-width='1'
                  fill-rule='evenodd'
                  transform='translate(12.000000, 40.000000)'>
                  <mask id='mask-1' fill='white'>
                    <use xlink:href='#path-1'></use>
                  </mask>
                  <use
                    id='Circle-Background'
                    fill='#E6E6E6'
                    xlink:href='#path-1'></use>
                  <g
                    id='Color/Palette/Blue-01'
                    mask='url(#mask-1)'
                    :fill=circleColor>
                    <rect id='????Color' x='0' y='0' width='240' height='240'></rect>
                  </g>
                </g>
                <mask id='mask-2' fill='white'>
                  <use xlink:href='#path-2' />
                </mask>
            </template>
              <g id='Mask' />
              <g
                id='Avataaar'
                stroke-width='1'
                fill-rule='evenodd'
                fill='black'
                mask='url(#mask-2)'>
                <g id='Body' transform='translate(32.000000, 36.000000)'>
                  <mask id='mask-silhouette' fill='white'>
                    <use xlink:href='#path-silhouette'></use>
                  </mask>
                  <use :fill="skinColor" xlink:href='#path-silhouette'></use>
                  <path
                    d='M156,79 L156,102 C156,132.927946 130.927946,158 100,158 C69.072054,158 44,132.927946 44,102 L44,79 L44,94 C44,124.927946 69.072054,150 100,150 C130.927946,150 156,124.927946 156,94 L156,79 Z'
                    id='Neck-Shadow'
                    fill-opacity="0.100000001"
                    fill='#000000'
                    mask='url(#mask-silhouette)'></path>
                </g>
                <g v-html="clothesType[clotheType]"></g>
                <g v-if="clotheType === 'GraphicShirt'" v-html="GraphicShirtTypes[graphicType]"></g>
                <g v-html="eyeTypes[eyeType]"></g>
                <g v-html="mouthTypes[mouthType]"></g>
                <g v-html="eyebrowTypes[eyebrowType]"></g>
                <g>
                  <g fill='black' transform='translate(76.000000, 82.000000)'>
                    <g
                      id='Nose/Default'
                      transform='translate(28.000000, 40.000000)'
                      opacity='0.16'>
                      <path
                        d='M16,8 C16,12.418278 21.372583,16 28,16 L28,16 C34.627417,16 40,12.418278 40,8'
                        id='Nose'>

                      </path>
                    </g>
                  </g>
                </g>
                <g v-html="topTypes[topType]"></g>
                <g v-html="facialHairTypes[facialHairType]"></g>
                <g v-html="accessoriesTypes[accessoriesType]"></g>
              </g>
            </g>
          </g>
        </g>
    </svg>
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
    export default {
         props: {
             isCircle: {
                type: Boolean,
                default: true
             },
             circleColor: {
                type: String,
                 default: '#6fb8e0'
            },
            topType: { type: String},
            accessoriesType: { type: String},
            facialHairType: { type: String},
            clotheType: { type: String},
            eyeType: { type: String},
            eyebrowType: { type: String},
            mouthType: { type: String},
            skinColor: { type: String},
            graphicType: { type: String},
            hairColor: { type: String},
            facialHairColor: { type: String},
            topColor: { type: String },
            clotheColor: { type: String},
         },
        data () {
            return {
                mouthTypes: mouthTypes,
                eyeTypes: eyeTypes,
                topTypes: topTypes,
                clothesType: clothesType,
                eyebrowTypes: eyebrowTypes,
                facialHairTypes: facialHairTypes,
                accessoriesTypes: accessoriesTypes,
                GraphicShirtTypes: GraphicShirtTypes,
            }
        },
    }
    </script>
    
    <style>
    </style>
    