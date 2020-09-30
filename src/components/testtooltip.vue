<template>
  <b-container>
    <b-row class="text-center">
      <b-col md="3" class="py-3">
        <b-button
          v-b-tooltip.hover
          :title="'Tip from title attribute ' + date"
          variant="success"
          >Title</b-button
        >
      </b-col>
      <b-col md="3" class="py-3">
        <b-button
          v-b-tooltip.hover="'String Tip'"
          v-b-tooltip.click="'String2 Tip'"
          variant="success"
          >String</b-button
        >
      </b-col>
      <b-col md="3" class="py-3">
        <b-button
          v-b-tooltip.hover.html="tipData"
          v-b-tooltip.click.html="tipMethod"
          variant="success"
          >Data</b-button
        >
      </b-col>
      <b-col md="3" class="py-3">
        <b-button
          id="popover-target-1"
          v-b-tooltip.hover.html="tipMethod"
          variant="success"
          >Method</b-button
        >

        <b-popover
          target="popover-target-1"
          triggers="click"
          placement="bottom"
        >
          <template v-slot:title>Popover Title</template>
          <testfrom/>
        </b-popover>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import testfrom from "./testfrom"
export default {
    components:{
        testfrom

    },
  data() {
    return {
      tipData: { title: "Tooltip <em>Message</em>" },
      date: new Date(),
      timer: null,
    };
  },
  mounted() {
    this.timer = setInterval(() => {
      this.date = new Date();
    }, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timer);
  },
  methods: {
    tipMethod() {
      // Note this is called each time the tooltip is first opened.
      return "<strong>" + new Date() + "</strong>";
    },
  },
};
</script>