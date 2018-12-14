<template src='./PartInfo.html'></template>
<style lang='scss' scoped src='./PartInfo.scss'></style>

<script>
import getPartsMixin from '../parts/get-parts-minxin';

export default {
  name: 'PartInfo',
  mixins: [getPartsMixin],
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
      return this.parts[partType].find(part => part.id === +id);
    },
  },
};
</script>
