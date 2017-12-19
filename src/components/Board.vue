<template>
  <svg class="board">
    <field v-for="(field, index) in fields" :key="field.id" :x="field.x" :y="field.y" :radius="field.radius" :type="field.type" :number="field.number" />
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
  width: 100%;
  height: 100%;
  position: relative;
}
</style>
