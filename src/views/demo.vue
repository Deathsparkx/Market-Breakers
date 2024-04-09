<template>
  <header class="header">
    <button>
      <img src="../assets/setting-icon.png" alt="" />
    </button>
  </header>
  <section class="sec-1">
    <div class="players">
      <div class="player-wrap">
        <img class="player-bg" src="../assets/player-bg.png" alt="" />
        <div class="player">
          <div class="player-img-wrap">
            <img class="player-img" src="../assets/p2.png" alt="" />
          </div>
          <div class="player-info">
            <div class="info">
              <span>Player 2</span>
              <div class="skill">
                <img src="../assets/p2-skill1.png" alt="" />
                <img src="../assets/p2-skill2.png" alt="" />
              </div>
            </div>
            <div class="amt">100,000 USD</div>
          </div>
        </div>
      </div>
      <div class="player-wrap">
        <img class="player-bg" src="../assets/player-bg.png" alt="" />
        <div class="player">
          <div class="player-img-wrap">
            <img class="player-img" src="../assets/p3.png" alt="" />
          </div>
          <div class="player-info">
            <div class="info">
              <span>Player 3</span>
              <div class="skill">
                <img src="../assets/p3-skill1.png" alt="" />
                <img src="../assets/p3-skill2.png" alt="" />
              </div>
            </div>
            <div class="amt">100,000 USD</div>
          </div>
        </div>
      </div>
      <div class="player-wrap">
        <img class="player-bg" src="../assets/player-bg.png" alt="" />
        <div class="player">
          <div class="player-img-wrap">
            <img class="player-img" src="../assets/p4.png" alt="" />
          </div>
          <div class="player-info">
            <div class="info">
              <span>Player 4</span>
              <div class="skill">
                <img src="../assets/p4-skill1.png" alt="" />
                <img src="../assets/p4-skill2.png" alt="" />
              </div>
            </div>
            <div class="amt">100,000 USD</div>
          </div>
        </div>
      </div>
    </div>
    <div class="graph-component">
      <!-- <img class="graph" src="../assets/graph.png" alt="" /> -->
      <img class="frame" src="../assets/graph-frame.png" alt="" />

      <LwChart
        :data="data"
        type="candlestick"
        :chartOptions="darkTheme.chart"
      />
    </div>
  </section>
  <section class="sec-2">
    <div class="sec-2-content">
      <div class="mode-wrap">
        <div class="status">Current Mode</div>
        <div class="mode">Low Stakes</div>
        <div class="mode">Ranked</div>
      </div>
      <div class="market-data">
        <div class="data-wrap">
          <div class="data">
            <div class="label">Current Price:</div>
            <div>{{ currentPrice }} USD</div>
          </div>
          <div class="data">
            <div class="label">All Time High:</div>
            <div>260.06 USD</div>
          </div>
          <div class="data">
            <div class="label">All Time Low:</div>
            <div>0.5052 USD</div>
          </div>
        </div>
        <div class="data-wrap">
          <div class="data">
            <div class="label">Month total Volume:</div>
            <div>445,571,039 SOL</div>
          </div>
          <div>
            <img class="meter" src="../assets/meter.png" alt="" />
          </div>
        </div>
      </div>
      <div class="event-wrap">
        <div class="market-event">
          <div v-for="i in eventList" class="event">
            <div>{{ i.date }} :</div>
            <div>{{ i.event }}</div>
          </div>
        </div>
      </div>
    </div>
  </section>
  <section class="sec-3">
    <div class="action-panel">
      <img class="action-bg" src="../assets/action-bg.png" alt="" />
      <div class="action-wrap">
        <div class="action-stats">
          <div class="status">Your Net Worth +17%</div>
          <div class="amt-wrap">
            {{ isNaN(userNetWorth.toFixed(2)) ? "-" : userNetWorth.toFixed(2) }}
          </div>
          <div class="amt-wrap-2">
            <div class="wrap">
              <div class="label">Amount:</div>
              <div class="amt">400.00 USD</div>
            </div>
            <!-- <div class="wrap">
              <div class="label">Limit:</div>
              <div class="amt">800.00</div>
            </div> -->
          </div>
        </div>
        <div class="action-buttons">
          <button class="limit" @click="marketType = !marketType">
            <img src="../assets/limit-icon.png" alt="" />
            <span v-if="marketType">Limit </span>
            <span v-else>Market</span>
          </button>
          <button class="buy" @click="buy()">Buy</button>
          <button class="sell" @click="sell()">Sell</button>
        </div>
      </div>
    </div>
    <div class="user-panel">
      <img class="stats-bg" src="../assets/stats-bg.png" alt="" />
      <div class="user-wrap">
        <div class="skill-wrap">
          <img src="../assets/stats-skill1.png" alt="" />
        </div>
        <div class="skill-wrap">
          <img class="skill2" src="../assets/stats-skill2.png" alt="" />
        </div>
        <div class="user-stats">
          <label for="">Assets:</label>
          <div class="amt">{{ userAssets.toFixed(2) }} SOL</div>
          <label for="">Your Funds:</label>
          <div class="amt">{{ userFunds.toFixed(2) }} USD</div>
        </div>
        <div class="user-icon">
          <img src="../assets/stats-user.png" alt="" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, reactive } from "vue";
import LwChart from "../components/lw-chart.vue";

var darkTheme = {
  chart: {
    layout: {
      background: {
        type: "solid",
        color: "#2B2B43",
      },
      lineColor: "#2B2B43",
      textColor: "#D9D9D9",
    },
    watermark: {
      color: "rgba(0, 0, 0, 0)",
    },
    crosshair: {
      color: "#758696",
    },
    grid: {
      vertLines: {
        color: "#2B2B43",
      },
      horzLines: {
        color: "#363C4E",
      },
    },
  },
  series: {
    topColor: "rgba(32, 226, 47, 0.56)",
    bottomColor: "rgba(32, 226, 47, 0.04)",
    lineColor: "rgba(32, 226, 47, 1)",
  },
};

const priceScaleOption = {
  precision: 8,
};

let array = [
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in SOL",
  },
];
let eventList = ref(array);

const data = ref([
  {
    open_time: 1706745600000,
    open: 96.96,
    high: 98.11,
    low: 93.11,
    close: 97.81,
    amount: 6556006.07,
    time: 1706831999999,
    volume: 627562058.6994,
    count: 652301,
    taker_buy_volume: 3228196.33,
    taker_buy_quote_volume: 309093273.8401,
    symbol: "SOL",
  },
  {
    open_time: 1706832000000,
    open: 97.81,
    high: 102.57,
    low: 97.39,
    close: 100.58,
    amount: 5487861.84,
    time: 1706918399999,
    volume: 548625813.6662,
    count: 580111,
    taker_buy_volume: 2751200.63,
    taker_buy_quote_volume: 275124077.6304,
    symbol: "SOL",
  },
  {
    open_time: 1706918400000,
    open: 100.57,
    high: 101.24,
    low: 96.53,
    close: 97.96,
    amount: 2787373.11,
    time: 1707004799999,
    volume: 274762025.0328,
    count: 292310,
    taker_buy_volume: 1382286.53,
    taker_buy_quote_volume: 136281901.0636,
    symbol: "SOL",
  },
  {
    open_time: 1707004800000,
    open: 97.95,
    high: 98.59,
    low: 95.08,
    close: 95.49,
    amount: 2914876.34,
    time: 1707091199999,
    volume: 282911440.8033,
    count: 295763,
    taker_buy_volume: 1423038.52,
    taker_buy_quote_volume: 138173035.8601,
    symbol: "SOL",
  },
  {
    open_time: 1707091200000,
    open: 95.48,
    high: 98.7,
    low: 94.11,
    close: 95.66,
    amount: 3891146.06,
    time: 1707177599999,
    volume: 375072768.1381,
    count: 381857,
    taker_buy_volume: 1964214.86,
    taker_buy_quote_volume: 189483103.3725,
    symbol: "SOL",
  },
  {
    open_time: 1707177600000,
    open: 95.66,
    high: 97.88,
    low: 92.88,
    close: 96.88,
    amount: 4279238.07,
    time: 1707263999999,
    volume: 408309176.2014,
    count: 407235,
    taker_buy_volume: 2154937.56,
    taker_buy_quote_volume: 205595782.4337,
    symbol: "SOL",
  },
  {
    open_time: 1707264000000,
    open: 96.87,
    high: 101.58,
    low: 94.62,
    close: 101.14,
    amount: 4577672.06,
    time: 1707350399999,
    volume: 446039059.9197,
    count: 489245,
    taker_buy_volume: 2329138.14,
    taker_buy_quote_volume: 227261096.6142,
    symbol: "SOL",
  },
  {
    open_time: 1707350400000,
    open: 101.14,
    high: 104.98,
    low: 100.51,
    close: 102.76,
    amount: 5082811.46,
    time: 1707436799999,
    volume: 521415121.7323,
    count: 574488,
    taker_buy_volume: 2548368.44,
    taker_buy_quote_volume: 261425100.1379,
    symbol: "SOL",
  },
  {
    open_time: 1707436800000,
    open: 102.77,
    high: 109.13,
    low: 102.76,
    close: 106.94,
    amount: 6686758.45,
    time: 1707523199999,
    volume: 705846559.5141,
    count: 724146,
    taker_buy_volume: 3467051.74,
    taker_buy_quote_volume: 366014739.0668,
    symbol: "SOL",
  },
  {
    open_time: 1707523200000,
    open: 106.94,
    high: 110.86,
    low: 106.86,
    close: 109.01,
    amount: 3939526.49,
    time: 1707609599999,
    volume: 429171975.2434,
    count: 451222,
    taker_buy_volume: 2005802.9,
    taker_buy_quote_volume: 218541100.5589,
    symbol: "SOL",
  },
  {
    open_time: 1707609600000,
    open: 109.01,
    high: 110.67,
    low: 107.24,
    close: 107.46,
    amount: 2755398.4,
    time: 1707695999999,
    volume: 300070898.8657,
    count: 337007,
    taker_buy_volume: 1329304.41,
    taker_buy_quote_volume: 144792952.7943,
    symbol: "SOL",
  },
  {
    open_time: 1707696000000,
    open: 107.46,
    high: 112.22,
    low: 103.4,
    close: 111.64,
    amount: 6169652.05,
    time: 1707782399999,
    volume: 665452212.1685,
    count: 684788,
    taker_buy_volume: 3098042.67,
    taker_buy_quote_volume: 334279630.3997,
    symbol: "SOL",
  },
  {
    open_time: 1707782400000,
    open: 111.65,
    high: 115.15,
    low: 108.25,
    close: 112.48,
    amount: 5622825.56,
    time: 1707868799999,
    volume: 631903077.7933,
    count: 674183,
    taker_buy_volume: 2771345.37,
    taker_buy_quote_volume: 311405826.2577,
    symbol: "SOL",
  },
  {
    open_time: 1707868800000,
    open: 112.49,
    high: 118.69,
    low: 110.61,
    close: 116.97,
    amount: 4884824.42,
    time: 1707955199999,
    volume: 563977441.6739,
    count: 593380,
    taker_buy_volume: 2535103.8,
    taker_buy_quote_volume: 292809396.4494,
    symbol: "SOL",
  },
  {
    open_time: 1707955200000,
    open: 116.97,
    high: 118.39,
    low: 111.51,
    close: 113.5,
    amount: 4927735.5,
    time: 1708041599999,
    volume: 567749563.9749,
    count: 658457,
    taker_buy_volume: 2277417.52,
    taker_buy_quote_volume: 262353178.7495,
    symbol: "SOL",
  },
  {
    open_time: 1708041600000,
    open: 113.5,
    high: 114.25,
    low: 107.94,
    close: 110.33,
    amount: 3947132.77,
    time: 1708127999999,
    volume: 438070793.2023,
    count: 521407,
    taker_buy_volume: 1907792.46,
    taker_buy_quote_volume: 211814412.4089,
    symbol: "SOL",
  },
  {
    open_time: 1708128000000,
    open: 110.32,
    high: 111.08,
    low: 105,
    close: 108.92,
    amount: 2897705.67,
    time: 1708214399999,
    volume: 314210779.8993,
    count: 388340,
    taker_buy_volume: 1328720.54,
    taker_buy_quote_volume: 144136048.8546,
    symbol: "SOL",
  },
  {
    open_time: 1708214400000,
    open: 108.92,
    high: 114.04,
    low: 107.51,
    close: 112.24,
    amount: 3083833.73,
    time: 1708300799999,
    volume: 343205223.4657,
    count: 414145,
    taker_buy_volume: 1589233.83,
    taker_buy_quote_volume: 176806018.0816,
    symbol: "SOL",
  },
  {
    open_time: 1708300800000,
    open: 112.25,
    high: 114.87,
    low: 110.75,
    close: 111.53,
    amount: 3746704.95,
    time: 1708387199999,
    volume: 422129836.0457,
    count: 514577,
    taker_buy_volume: 1822769.11,
    taker_buy_quote_volume: 205431020.3446,
    symbol: "SOL",
  },
  {
    open_time: 1708387200000,
    open: 111.53,
    high: 112.11,
    low: 103,
    close: 108.31,
    amount: 5676734.13,
    time: 1708473599999,
    volume: 614703000.8099,
    count: 732595,
    taker_buy_volume: 2793426.7,
    taker_buy_quote_volume: 302432954.1955,
    symbol: "SOL",
  },
  {
    open_time: 1708473600000,
    open: 108.32,
    high: 108.4,
    low: 100.23,
    close: 105.03,
    amount: 4752688.01,
    time: 1708559999999,
    volume: 493622986.4706,
    count: 638631,
    taker_buy_volume: 2247491.44,
    taker_buy_quote_volume: 233441642.5679,
    symbol: "SOL",
  },
  {
    open_time: 1708560000000,
    open: 105.04,
    high: 107.1,
    low: 101.53,
    close: 101.76,
    amount: 3905642.33,
    time: 1708646399999,
    volume: 408028903.1197,
    count: 532651,
    taker_buy_volume: 2017092.37,
    taker_buy_quote_volume: 210745180.8383,
    symbol: "SOL",
  },
  {
    open_time: 1708646400000,
    open: 101.75,
    high: 103.1,
    low: 98.64,
    close: 99.9,
    amount: 3546853.99,
    time: 1708732799999,
    volume: 359325149.9384,
    count: 441289,
    taker_buy_volume: 1746511.02,
    taker_buy_quote_volume: 176969708.6294,
    symbol: "SOL",
  },
  {
    open_time: 1708732800000,
    open: 99.91,
    high: 104.85,
    low: 98.48,
    close: 104.01,
    amount: 2334116.02,
    time: 1708819199999,
    volume: 237972991.0225,
    count: 300412,
    taker_buy_volume: 1238506.3,
    taker_buy_quote_volume: 126296954.4945,
    symbol: "SOL",
  },
  {
    open_time: 1708819200000,
    open: 104.02,
    high: 104.43,
    low: 102,
    close: 103.47,
    amount: 1967184.81,
    time: 1708905599999,
    volume: 202983222.2078,
    count: 285185,
    taker_buy_volume: 933488.17,
    taker_buy_quote_volume: 96331564.6463,
    symbol: "SOL",
  },
  {
    open_time: 1708905600000,
    open: 103.47,
    high: 110.89,
    low: 100.29,
    close: 109.9,
    amount: 5392138.71,
    time: 1708991999999,
    volume: 570413289.4648,
    count: 723403,
    taker_buy_volume: 2824015.44,
    taker_buy_quote_volume: 298794797.9401,
    symbol: "SOL",
  },
  {
    open_time: 1708992000000,
    open: 109.9,
    high: 112.3,
    low: 105.29,
    close: 108.36,
    amount: 6198163.52,
    time: 1709078399999,
    volume: 679932921.2006,
    count: 910828,
    taker_buy_volume: 3061442.24,
    taker_buy_quote_volume: 335848421.7037,
    symbol: "SOL",
  },
  {
    open_time: 1709078400000,
    open: 108.35,
    high: 119.06,
    low: 106.85,
    close: 119.03,
    amount: 11832282.01,
    time: 1709164799999,
    volume: 1332835060.4958,
    count: 1812047,
    taker_buy_volume: 6046391.03,
    taker_buy_quote_volume: 681766965.7258,
    symbol: "SOL",
  },
  {
    open_time: 1709164800000,
    open: 119.03,
    high: 134.65,
    low: 117.15,
    close: 125.68,
    amount: 13847087.32,
    time: 1709251199999,
    volume: 1758043857.4217,
    count: 2407149,
    taker_buy_volume: 7077792.29,
    taker_buy_quote_volume: 898386234.6854,
    symbol: "SOL",
  },
]);

formatDataTime();

function formatDataTime() {
  data.value.forEach((item) => {
    item.time = timestampToDate(item.time);

    return item;
  });
}

function timestampToDate(timestamp) {
  // Create a new Date object with the timestamp
  const date = new Date(timestamp);

  // Get the components of the date
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0"); // Months are zero-based
  const day = String(date.getDate()).padStart(2, "0");
  const hours = String(date.getHours()).padStart(2, "0");
  const minutes = String(date.getMinutes()).padStart(2, "0");
  const seconds = String(date.getSeconds()).padStart(2, "0");

  // Construct the date string in the desired format
  const formattedDate = `${year}-${month}-${day}`;

  return formattedDate;
}

function generateNextCandlestick(data) {
  // Get the last entry in the data
  const lastEntry = data[data.length - 1];

  // Calculate the time for the next candlestick (assuming 1 day interval)
  const nextOpenTime = lastEntry.open_time + 24 * 60 * 60 * 1000; // Adding 1 day in milliseconds

  // Generate random price movement within a certain range
  const priceChange = Math.random() * 5 - 2.5; // Random change between -2.5 and +2.5
  const nextOpenPrice = lastEntry.close + priceChange;
  const nextClosePrice = nextOpenPrice + (Math.random() * 10 - 5); // Random close price within +/- 5 of open price

  // Generate the next candlestick data
  const nextCandlestick = {
    open_time: nextOpenTime,
    open: nextOpenPrice,
    high: Math.max(nextOpenPrice, nextClosePrice),
    low: Math.min(nextOpenPrice, nextClosePrice),
    close: nextClosePrice,
    amount: 0, // Placeholder values, you might need to adjust these based on your actual data
    time: timestampToDate(nextOpenTime + 24 * 60 * 60 * 1000), // Assuming a duration of 1 day for the next candlestick
    volume: 0,
    count: 0,
    taker_buy_volume: 0,
    taker_buy_quote_volume: 0,
    symbol: lastEntry.symbol, // Reusing the same symbol
  };

  return nextCandlestick;
}

// Usage example:
const nextCandlestick = generateNextCandlestick(data.value);
console.log(nextCandlestick);

setInterval(() => {
  const nextCandlestick = generateNextCandlestick(data.value);

  data.value.push(nextCandlestick);

  let newList = [...data.value];

  // // console.log(newList);

  data.value = newList;
  currentPrice.value = data.value[data.value.length - 1].close.toFixed(2);
  netWorth.value = userAssets.value * currentPrice.value;


  // console.log(data.value[data.value.length - 1].time);
}, 1000);

//Set initial current price
let currentPrice = ref(data.value[data.value.length - 1].close);

//User data
let userFunds = ref(100000);
let userAssets = ref(0);
let netWorth = ref(userAssets * currentPrice);
let userNetWorth = ref(netWorth);
let marketType = ref(true);

function buy() {
  console.log("buy");
  if(userFunds.value > parseInt(currentPrice.value)  ){
    userAssets.value = userAssets.value + 1;
    userFunds.value = userFunds.value - currentPrice.value  ;
    console.log(netWorth.value);
  }  
}

function sell() {
  if(userAssets.value > 0){
    userAssets.value = userAssets.value - 1;
    console.log(userFunds.value, currentPrice.value)
    userFunds.value = userFunds.value + parseInt(currentPrice.value)   ;
    console.log(netWorth.value);
  }  
}
</script>

<style lang="scss" scoped>
.header {
  background-color: black;
  padding: 10px;

  button {
    background: none;
    border: none;
    width: 40px;

    img {
      max-width: 100%;
    }
  }
}

section {
  max-width: 1400px;
  margin: auto;
}

.sec-1 {
  display: flex;
  gap: 1.5vw;
  .players {
    width: 20%;
    margin-top: 4%;
    .player-wrap {
      position: relative;
    }

    .player-bg {
      width: 100%;
    }
    .player {
      position: absolute;
      top: 0;
      left: 0;
      padding: 0.8vw;
      display: flex;

      .player-img-wrap {
        width: 43%;
      }
      .player-img {
        max-width: 100%;
      }

      .info {
        display: flex;
        justify-content: space-between;
        margin-right: 5%;
        span {
          font-weight: bold;
        }

        img {
          width: 100%;
        }

        .skill {
          display: flex;
          justify-content: end;
          gap: 20%;
          width: 15%;
        }
      }

      .amt {
        padding-top: 5px;
        padding-left: 5%;
      }
      color: white;
      font-size: 1vw;
    }
  }
  .graph-component {
    margin-top: -1%;
    width: 60%;
    // height: 43vh;
    background: black;
    position: relative;

    img {
      position: absolute;
    }

    .frame {
      width: 100%;
      z-index: 10;
    }

    .graph {
      width: 100%;
      top: 0;
      left: 0;
      // transform: translate(-50%, -50%);
    }
  }
}

.sec-2 {
  margin-top: 5%;

  .sec-2-content {
    max-width: 90%;
    // margin: auto;
    display: flex;
    max-height: 200px;

    .mode-wrap {
      background-image: linear-gradient(180deg, #5a6a7e, #5a6a7e, #323a46);
      border-radius: 10px;
      text-align: center;
      width: 450px;
      margin-right: 2%;
      display: flex;
      flex-direction: column;
      // justify-content: center;
      padding-top: 20px;
      align-items: center;

      .status {
        color: #00ff3c;
        font-weight: bold;
        font-size: 26px;
        text-shadow: 0px 0px 8.6px #00ff3c;
      }

      .mode {
        font-size: 22px;
        color: white;
        width: 100%;
        background-color: #1e1e1e;
        border-radius: 10px;
        padding: 4px 10px;
        margin-top: 16px;
        width: 80%;
        text-align: center;
        box-shadow: inset 0px 2px 4px 0px #000000;
        text-shadow: 0px 0px 8.5px rgba(0, 213, 255, 0.69);
      }
    }

    .market-data {
      color: white;
      background: rgba(255, 255, 255, 0.1);
      width: 45%;
      display: flex;
      font-size: 23px;
      font-weight: bold;
      padding: 2.5%;
      border-radius: 10px;
      margin-right: 2%;

      .data-wrap {
        width: 100%;
        .label {
          font-size: 14px;
        }

        .meter {
          margin-top: 5%;
        }

        .data {
          margin-bottom: 5%;
        }
      }
      img {
        width: 100%;
      }
    }

    .event-wrap {
      border-radius: 10px;
      background: rgba(255, 255, 255, 0.1);
      padding: 1%;
      width: 60%;
    }

    .market-event {
      max-height: 100%;
      overflow-y: scroll;
      padding-right: 10px;
      display: flex;
      flex-direction: column-reverse;

      .event {
        display: flex;
        gap: 5px;
        border-bottom: 1px solid rgba(255, 255, 255, 0.5);
        color: rgba(255, 255, 255, 0.5);
        padding: 10px;
      }

      .event:first-child {
        border: none;
        color: white;
      }
    }
  }
}

.sec-3 {
  margin-top: 1%;

  display: flex;
  justify-content: space-between;

  .action-panel {
    position: relative;
    height: 200px;
    // width: 800px;

    .action-bg {
      height: 100%;
    }

    .action-wrap {
      position: absolute;
      bottom: 0;
      display: flex;
      align-items: end;
      height: 100%;

      .action-stats {
        width: 340px;
        height: 100%;
        // background-color: lightblue;
        display: flex;
        flex-direction: column;
        justify-content: end;
        margin: 30px;

        .status {
          color: #00ff3c;
          font-weight: bold;
          font-size: 26px;
          text-shadow: 0px 0px 8.6px #00ff3c;
        }

        .amt-wrap {
          font-size: 22px;
          color: white;
          width: 100%;
          background-color: #1e1e1e;
          border-radius: 10px;
          padding: 4px 10px;
          margin: 16px 0;
          width: 80%;
          text-align: center;
          text-shadow: 0px 0px 8.5px rgba(0, 213, 255, 0.69);
        }
        .amt-wrap-2 {
          display: flex;
          gap: 10px;

          .wrap {
            width: 50%;
            .label {
              font-size: 16px;
              color: white;
            }

            .amt {
              font-size: 22px;
              color: white;
              //   width: 100%;
              background-color: #1e1e1e;
              border-radius: 10px;
              padding: 4px 20px;
              text-shadow: 0px 0px 8.5px rgba(0, 213, 255, 0.69);
            }
          }
        }
      }

      .action-buttons {
        margin-left: -120px;
        height: 100%;
        display: flex;
        align-items: end;
        padding-bottom: 25px;
        gap: 20px;
        button {
          border-radius: 10px;
          color: white;
          font-size: 22px;
          text-transform: uppercase;
          width: 120px;
          padding: 6px 0;
          box-shadow: 0px 2px 4px 0px #00000077;
          border: none;
          height: 42px;
          font-weight: bold;
        }

        button:active {
          box-shadow: inset 1px 1px 4px 0px #000000;
        }

        .limit {
          text-transform: capitalize;
          display: flex;
          align-items: center;
          gap: 10px;
          font-size: 18px;
          justify-content: center;
          background-image: linear-gradient(180deg, #00e0ff, #004699);

          img {
            width: 20px;
          }
        }

        .buy {
          // background-color: #009924;
          background-image: linear-gradient(180deg, #00ff3c, #009924);
        }

        .sell {
          background-color: red;
        }
      }
    }
  }

  .user-panel {
    position: relative;
    // width: 620px;
    height: 200px;
    display: flex;
    justify-content: end;
    align-items: end;

    .stats-bg {
      height: 100%;
    }

    .user-wrap {
      position: absolute;
      top: 0;
      right: 0;
      display: flex;
      width: 100%;
      height: 100%;
      justify-content: end;
      align-items: end;

      .skill-wrap {
        width: 70px;
        margin: 16px 10px;
      }

      .skill-wrap img {
        width: 100%;
      }

      .skill-wrap .skill2 {
        box-shadow: 0px 0px 10px 0px #00ff38;
      }

      .user-stats {
        margin: 10px;
      }

      .user-icon {
        width: 160px;
        height: 100%;
        display: flex;
        align-items: center;
        padding-right: 10px;
      }

      .user-icon img {
        width: 100%;
      }

      label {
        color: white;
        font-size: 16px;
        margin-top: 10px;
      }

      .amt {
        font-size: 18px;
        color: #ffc629;
        background-color: #1e1e1e;
        border-radius: 10px;
        padding: 4px 20px;
        margin-bottom: 10px;
        text-align: end;
      }
    }
  }
}
</style>
