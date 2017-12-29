<template>
  <svg class="board" viewBox="0 0 600 520">
    <defs>
      <filter id="f1" x="0" y="0">
        <feGaussianBlur in="SourceGraphic" stdDeviation="1" />
      </filter>
      <pattern id="img-wood" x="0" y="0" height="100%" width="100%" viewBox="0 0 700 800">
        <image href="/static/wood.jpg"></image>
      </pattern>
      <pattern id="img-stone" x="0" y="0" height="100%" width="100%" viewBox="0 0 350 400">
        <image href="/static/stone.jpg"></image>
      </pattern>
      <pattern id="img-desert" x="0" y="0" height="100%" width="100%" viewBox="0 0 350 400">
        <image href="/static/desert.jpg"></image>
      </pattern>
      <pattern id="img-sheep" x="0" y="0" height="100%" width="100%" viewBox="0 0 170 200">
        <image href="/static/sheep.jpg"></image>
      </pattern>
      <pattern id="img-clay" x="0" y="0" height="100%" width="100%" viewBox="0 0 170 200">
        <image href="/static/clay.jpg"></image>
      </pattern>
      <pattern id="img-cereal" x="0" y="0" height="100%" width="100%" viewBox="0 0 170 200">
        <image href="/static/cereal.jpg"></image>
      </pattern>
    </defs>
    <field v-for="field in fields" :key="field.id" :x="field.x" :y="field.y" :radius="field.radius" :type="field.type" :number="field.number" />
  </svg>
</template>

<script>
import boards from '../model/boards'

export default {
  name: 'Board',
  beforeMount () {
    this.board = boards[Math.floor(Math.random() * boards.length)]
    this.fields = this.board.fields
    let desert
    const types = [
      'desert',
      'clay', 'clay', 'clay',
      'stone', 'stone', 'stone',
      'sheep', 'sheep', 'sheep', 'sheep',
      'cereal', 'cereal', 'cereal', 'cereal',
      'wood', 'wood', 'wood', 'wood'
    ].sort(() => 0.5 - Math.random())
    types.forEach((v, i) => {
      if (v === 'desert') {
        desert = this.fields[i]
      }
      this.fields[i].type = v
    })
    const numbers = [
      2,
      3, 3,
      4, 4,
      5, 5,
      6, 6,
      7,
      8, 8,
      9, 9,
      10, 10,
      11, 11,
      12
    ].sort(() => 0.5 - Math.random())
    let seven
    numbers.forEach((v, i) => {
      if (v === 7) {
        seven = this.fields[i]
      }
      this.fields[i].number = v
    })
    seven.number = desert.number
    desert.number = 7
  },
  components: {
    field: () => import('@/components/Field')
  },
  data () {
    return {
      board: [],
      fields: []
    }
  },
  methods: {}
}
</script>

<style scoped>
.board {
  width: 800px;
  height: 720px;
}
</style>
