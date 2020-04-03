<template>
  <v-card flat class="pr-1">
    <v-card-title>{{ title }}</v-card-title>
    <apexchart
      type="bar"
      width="100%"
      height="300"
      :series="series"
      :options="chartOptions"
    />
  </v-card>
</template>
<script>
export default {
  props: [
    "title",
    "series",
    "grid",
    "tooltip",
    "colors",
    "labels",
    "labelFormatter",
    "stacked",
    "horizontal",
    "showDataLabel"
  ],
  data() {
    const colors = this.$props.colors;
    const grid = this.$props.grid;
    const tooltip = this.$props.tooltip;
    const labelFormatter = this.$props.labelFormatter;

    return {
      chartOptions: {
        chart: {
          type: "bar",
          height: 300,
          stacked: this.$props.stacked
        },
        plotOptions: {
          bar: {
            horizontal: this.$props.horizontal,
            columnWidth: "55%",
            endingShape: "rounded"
          }
        },
        title: { text: undefined, align: "center", floating: true },
        dataLabels: {
          enabled: this.$props.showDataLabel,
          textAnchor: "middle"
        },
        xaxis: {
          categories: this.$props.labels,
          ...(labelFormatter
            ? {
                labels: {
                  formatter: labelFormatter
                }
              }
            : {})
        },
        ...(colors ? { colors } : {}),
        ...(grid ? { grid } : {}),
        ...(tooltip ? { tooltip } : {})
      }
    };
  },
  mounted() {}
};
</script>
