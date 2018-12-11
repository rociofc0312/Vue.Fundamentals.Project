<template src='./RobotBuilder.html'></template>
<style lang="scss" scoped src='./RobotBuilder.scss'></style>

<script>
import availableParts from '../../data/parts';

function getPreviousValidIndex(index, lenght) {
  const deprecatedIndex = index - 1;
  return deprecatedIndex < 0 ? lenght - 1 : deprecatedIndex;
}

function getNextValidIndex(index, lenght) {
  const incrementedIndex = index + 1;
  return incrementedIndex > lenght - 1 ? 0 : incrementedIndex;
}

export default {
  name: 'RobotBuilder',
  data() {
    return {
      availableParts,
      selectedHeadIndex: 0,
      cart: [],
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
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIndex],
        leftArm: availableParts.arms[this.selectedHeadIndex],
        rightArm: availableParts.arms[this.selectedHeadIndex],
        torso: availableParts.torsos[this.selectedHeadIndex],
        bases: availableParts.bases[this.selectedHeadIndex],
      };
    },
  },
  methods: {
    selectNextHead() {
      this.selectedHeadIndex = getNextValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    selectPreviousHead() {
      this.selectedHeadIndex = getPreviousValidIndex(
        this.selectedHeadIndex,
        availableParts.heads.length,
      );
    },
    addToCart() {
      const robot = this.selectedRobot;
      const cost = robot.head.cost
        + robot.leftArm.cost
        + robot.torso
        + robot.rightArm
        + robot.bases;
      this.cart.push(Object.assign({}, robot, { cost }));
    },
  },
};
</script>
