<template>
  
    <div class="pro" 
    :class="[
    `pro--${type}`
    ]">
      <div class="pro-line" v-if="type == 'line'">
        <div
          class="pro-line__outer"
          :style="{height:strokeWidth+'px'}"
        >
          <div
            class="pro-line__inner"
            :style="barStyle"
          >
            <div
              v-if="textInside && showText"
              class="pro__inner-text"
            >
              {{percentage}}%
            </div>
          </div>
        </div>
      </div>
      <div class="pro-circle" v-if="type == 'circle'" :style="{width:width+'px'}">
        <svg viewBox='0 0 100 100'>
          <path
          
            :d='pathD'
            fill='none'
            :stroke-width='relativeStrokeWidth'
            stroke="#ddd"

          ></path>
          <path
            :d='pathD'
            fill='none'
            :stroke-width='relativeStrokeWidth'
            :stroke="barColor"
            :style="circleStyle"
            stroke-linecap='round'
          ></path>
        </svg>
      </div>
      <div
        v-if="!textInside && showText"
        class="pro-text"
      >
        <!-- 90% -->
        <template v-if="!status">{{percentage}}%</template>
        <i
          v-else
          class="lhfont"
          :style="{color:barColor}"
          :class="iconClass"

        ></i>
      </div>
    </div>

</template>

<script>
export default {
  props: {
    strokeWidth: {
      type: Number,
      default: 6
    },
    percentage: {
      type: Number,
      required: true,
      default: 0,
      validator: val => val >= 0 && val <= 100
    },
    status: {
      type: String,
      validator: val => ["success", "false"].includes(val)
    },
    type: {
      type: String,
      default: "line",
      validator: val => ["line", "circle"].includes(val)
    },
    textInside: {
      type: Boolean,
      default: false
    },
    showText: {
      type: Boolean,
      default: true
    },
    color:{
        type:String,
    },
    width:{
      type:Number,
      default:126
    }
  },
  computed: {
    perimiter(){
      const radius = 50 - this.relativeStrokeWidth / 2
      return 2 * Math.PI * radius
    },
    circleStyle(){
      const perimiter = this.perimiter
      return {
        strokeDasharray:`${perimiter}px,${perimiter}px`,
        strokeDashoffset:(1 - this.percentage/100) * perimiter + 'px'
      }
    },
    relativeStrokeWidth(){
      return this.strokeWidth * 100 / this.width
    },
    pathD(){
      const radius = 50 - this.relativeStrokeWidth / 2
      return `M 50 50 m 0 -${radius} 
      a ${radius} ${radius} 0 1 1 0 ${radius * 2} 
      a ${radius} ${radius} 0 1 1 0 -${radius * 2}`
    },
    barColor() {
      let color;
      if(this.color){
          return this.color
      }
      switch (this.status) {
        case "success":
          color = "#13ce66";
          break;
        case "false":
          color = "#ff4949";
          break;
        default:
          color = "#20a0ff";
          break;
      }
      return color;
    },
    barStyle() {
      return {
        height: this.strokeWidth + "px",
        width: this.percentage + "%",
        backgroundColor: this.barColor
      };
    },
    iconClass() {
      if (this.type == "line") {
        return this.status == "success"
          ? "icon-circle-success"
          : "icon-circle-false";
      } else {
        return this.status == "success" ? "icon-success" : "icon-false";
      }
    }
  }
};
</script>

<style>
@font-face {
  font-family: "lhfont"; /* project id 1205412 */
  src: url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.eot");
  src: url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.eot?#iefix")
      format("embedded-opentype"),
    url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.woff2") format("woff2"),
    url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.woff") format("woff"),
    url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.ttf") format("truetype"),
    url("//at.alicdn.com/t/font_1205412_okmjhpfcv5r.svg#iconfont") format("svg");
}
.lhfont {
  font-family: "lhfont" !important;
  font-size: 16px;
  font-style: normal;
}
.icon-circle-success::before {
  content: "\e663";
}
.icon-circle-false::before {
  content: "\e606";
}
.icon-success::before {
  content: "\e742";
}
.icon-false::before {
  content: "\e615";
}

.pro-line {
  width: 95%;
  /* background-color: #d32d2d; */
  padding-right: 50px;
  margin-right: -50px;
  display: inline-block;
}
.pro-line__outer {
  width: 100%;
  background-color: #ddd;
  border-radius: 100px;
}
.pro-line__inner {
  border-radius: 100px;
  text-align: right;
  line-height: 1;
}
.pro-text {
  display: inline-block;
  width: 4%;
  margin-left: 1%;
}
.pro__inner-text {
  color: #fff;
  font-size: 12px;
  display: inline-block;
  margin: 0 5px;
  vertical-align: middle;
}
.pro--circle{
  display: inline-block;
  position:relative;

}
.pro--circle .pro-text {
  position:absolute;
  top:50%;
  transform:translateY(-50%);
  width:100%;
  text-align:center;
  margin:0;
}
</style>