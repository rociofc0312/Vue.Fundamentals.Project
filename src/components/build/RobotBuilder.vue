<template src='./RobotBuilder.html'></template>
<style lang='scss' scoped src='./RobotBuilder.scss'></style>

<script>
import PartSelector from '../part-selector/PartSelector.vue';
import CollapsibleSection from '../shared/CollapsibleSection.vue';

export default {
  name: 'RobotBuilder',
  created() {
    this.$store.dispatch('robots/getParts');
  },
  beforeRouteLeave(to, from, next) {
    if (this.addedToCart) {
      next(true);
    } else {
      /* eslint no-alert: 0 */
      /* eslint no-restricted-globals: 0 */
      const response = confirm('Are you sure ou want to leave?');
      next(response);
    }
  },
  components: { PartSelector, CollapsibleSection },
  data() {
    return {
      addedToCart: false,
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
    availableParts() {
      return this.$store.state.robots.parts;
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
      this.$store.dispatch('robots/addRobotToCart', Object.assign({}, robot, { cost }))
        .then(() => this.$router.push('/cart'));
      this.addedToCart = true;
    },
  },
};
// You commit a mutation and dispatch an action
</script>
