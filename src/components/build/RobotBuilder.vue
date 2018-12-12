<template src='./RobotBuilder.html'></template>
<style lang='scss' scoped src='./RobotBuilder.scss'></style>

<script>
import availableParts from '../../data/parts';
import PartSelector from '../part-selector/PartSelector.vue';
import CollapsibleSection from '../shared/CollapsibleSection.vue';

export default {
  name: 'RobotBuilder',
  components: { PartSelector, CollapsibleSection },
  data() {
    return {
      availableParts,
      cart: [],
      selectedRobot: {
        head: {},
        leftArm: {},
        rightArm: {},
        torso: {},
        bases: {},
      },
    };
  },
  computed: {
    saleBorderClass() {
      return this.selectedRobot.head.onSale ? 'sale-border' : '';
    },
    headBorderStyle() {
      return {
        border: this.selectedRobot.head.onSale
          ? '3px solid red'
          : '3px solid #aaa',
      };
    },
  },
  methods: {
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
      + robot.leftArm.cost
      + robot.torso.cost
      + robot.rightArm.cost
      + robot.bases.cost;
      this.cart.push(Object.assign({}, robot, { cost }));
    },
  },
};
</script>
