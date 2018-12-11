<template src="./RobotBuilder.html"></template>
<style src="./RobotBuilder.css"></style>

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
    };
  },
  computed: {
    selectedRobot() {
      return {
        head: availableParts.heads[this.selectedHeadIndex],
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
  },
};
</script>
