/**
 *  CREATED AT 2022.10.12
 *  CREATED BY webstar0411@gmail.com
 */

<template>
  <div style="width: 100%; height: 100vh" id="organization-chart"></div>
</template>

<script>
import OrgChart from "./plugin/orgchart";

export default {
  props: {
    data: Object,
  },

  emits: ["onUpdate"],

  mounted() {
    const _this = this;

    // initialize chart handler
    const chart = new OrgChart(document.getElementById("organization-chart"), {
      nodes: this.$props.data,
      enableDragDrop: true,
      template: "rony",
      nodeBinding: {
        field_0: "name",
        field_1: "position",
        img_0: "avatar",
      },
      editForm: { titleBinding: "name", photoBinding: "avatar" },
    });

    // handles update event
    chart.on("update", function (sender, oldNode, newNode) {
      sender.updateNode(newNode);
      _this.$emit("onUpdate", newNode);
      return false;
    });
  },
};
</script>