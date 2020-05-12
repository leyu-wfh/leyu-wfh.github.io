<template>
  <div>
    <!-- <button v-on:click="count++">You clicked me {{ count }} times.</button> -->
    <Plotly :data="data" :layout="layout" :display-mode-bar="true"></Plotly>
  </div>
</template>
<script>
import { Plotly } from "vue-plotly";
import axios from "axios";
export default {
  components: {
    Plotly
  },
  data: function() {
    return {
      data: [],
      layout: { title: "Actual data from Alapha Vantage API for USDJPY" },
      count: 0
    };
  },
  mounted: function() {
    axios
      .get(
        "https://www.alphavantage.co/query?function=FX_DAILY&from_symbol=USD&to_symbol=JPY&apikey=V388HX66BU7OW6MR"
      )
      .then(resp => {
        var timeseries = resp.data["Time Series FX (Daily)"];
        const [dates, open, high, low, close] = this.getDatesOpenHighLowClose(
          timeseries
        );
        console.log(dates);
        this.data = [
          {
            decreasing: { line: { color: "#7F7F7F" } },
            increasing: { line: { color: "#17BECF" } },
            line: { color: "rgba(31,119,180,1)" },
            type: "candlestick",
            xaxis: "x",
            yaxis: "y",

            x: dates,
            open: open,
            high: high,
            low: low,
            close: close
          }
        ];
        this.layout = {
          dragmode: "zoom",
          margin: {
            r: 10,
            t: 25,
            b: 40,
            l: 60
          },
          showlegend: false,
          xaxis: {
            autorange: true,
            title: "Date",
            type: "date"
          },
          yaxis: {
            autorange: true,
            type: "linear"
          }
        };
        // console.log(this.dataset);
      });
  },
  methods: {
    getDatesOpenHighLowClose: function(timeseries) {
      var dates = [];

      var open = [];
      var high = [];
      var low = [];
      var close = [];
      Object.keys(timeseries).forEach(date => {
        dates.push(date);
        var candle = timeseries[date];
        open.push(candle["1. open"]);
        high.push(candle["2. high"]);
        low.push(candle["3. low"]);
        close.push(candle["4. close"]);
      });
      return [dates, open, high, low, close];
    }
  }
};
</script>
