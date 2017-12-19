<template>
  <svg class="field">
    <polygon :points="points" :class="type"/>
    <text :x="x" :y="y" :style="{ fontSize: this.fontSize }">{{ number }}</text>
  </svg>
</template>

<script>
export default {
  name: 'Field',
  props: {
    x: {
      type: Number,
      required: true
    },
    y: {
      type: Number,
      required: true
    },
    radius: {
      type: Number,
      default: 60
    },
    type: {
      type: String,
      default: 'desert'
    },
    number: {
      type: Number,
      default: 7
    },
    styles: {
      type: Object,
      default () {
        return {
          fontSize: `${14}px`
        }
      }
    }
  },
  mounted () {
    for (let i = 0; i < 6; i++) {
      this.points += `${this.x1(i)},${this.y1(i)} `
    }
  },
  computed: {
    fontSize (x) {
      return `${-2 * Math.abs(this.number - 7, 2) + 20}px`
    }
  },
  components: {
    field: () => import('@/components/Field')
  },
  data () {
    return {
      points: ''
    }
  },
  methods: {
    angle (i) {
      return (Math.PI / 3) * i
    },
    x1 (i) {
      return Math.round(this.radius * Math.sin(this.angle(i)) + this.x)
    },
    y1 (i) {
      return Math.round(this.radius * Math.cos(this.angle(i)) + this.y)
    }
  }
}
</script>

<style scoped>
.field {
  text-align: center;
}
.locked {
  fill: aquamarine;
}
.stone {
  fill: #858585;
}
.sheep {
  fill: #acfc94;
}
.cereal {
  fill: #f7c77f;
}
.wood {
  fill: #09440b;
}
.clay {
  fill: #47280a;
}
.desert {
  fill: #ffebd6;
}
text {
  fill: #ffffff;
  font-weight: 777; 
  text-shadow: 0px 0px 3px #000000;
  text-anchor: middle; 
  alignment-baseline: central;
}
</style>
