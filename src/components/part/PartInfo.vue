<template src='./PartInfo.html'></template>
<style lang='scss' scoped src='./PartInfo.scss'></style>

<script>
import parts from '../../data/parts';

export default {
  name: 'PartInfo',
  props: {
    partType: { type: String },
    id: {
      type: [Number, String],
      validator(value) {
        return Number.isInteger(Number(value));
      },
    },
  },
  computed: {
    part() {
      const { partType, id } = this;
      return parts[partType].find(part => part.id === +id);
    },
  },
};
</script>
