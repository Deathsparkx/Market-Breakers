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
            <div class="amt">100,00 USD</div>
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
            <div class="amt">100,00 USD</div>
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
            <div class="amt">100,00 USD</div>
          </div>
        </div>
      </div>
    </div>
    <div class="graph-component">
      <img class="frame" src="../assets/graph-frame.png" alt="" />
      <img class="graph" src="../assets/graph.png" alt="" />
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
            <div>523.99 USD</div>
          </div>
          <div class="data">
            <div class="label">All Time High:</div>
            <div>523.99 USD</div>
          </div>
          <div class="data">
            <div class="label">All Time Low:</div>
            <div>523.99 USD</div>
          </div>
        </div>
        <div class="data-wrap">
          <div class="data">
            <div class="label">Month total Volume:</div>
            <div>3.23 PEPE</div>
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
          <div class="amt-wrap">423,123.12</div>
          <div class="amt-wrap-2">
            <div class="wrap">
              <div class="label">Amount:</div>
              <div class="amt">400.00</div>
            </div>
            <!-- <div class="wrap">
              <div class="label">Limit:</div>
              <div class="amt">800.00</div>
            </div> -->
          </div>
        </div>
        <div class="action-buttons">
          <button class="limit">
            <img src="../assets/limit-icon.png" alt="">
            Limit
          </button>
          <button class="buy">Buy</button>
          <button class="sell">Sell</button>
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
          <div class="amt">0.005 PEPE</div>
          <label for="">Your Funds:</label>
          <div class="amt">1235.21 USD</div>
        </div>
        <div class="user-icon">
          <img src="../assets/stats-user.png" alt="" />
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from "vue";

let array = [
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
  {
    date: "22/05/2024",
    event: "A hacker has found an exploit in pepecoins",
  },
];
let eventList = ref(array);
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
      font-size: 1.1vw;
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
        text-shadow: 0px 0px 8.6px #00FF3C;

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
      width: 40%;
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
          text-shadow: 0px 0px 8.6px #00FF3C;
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

        .limit{
          text-transform: capitalize;
          display: flex;
          align-items: center;
          gap: 10px;
          font-size: 18px;
          justify-content: center;
          background-image: linear-gradient(180deg, #00E0FF, #004699);
          
          img{
            width: 20px;
          }
        }

        .buy {
          // background-color: #009924;
          background-image: linear-gradient(180deg, #00FF3C, #009924);
          
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

      .skill-wrap .skill2{
        box-shadow: 0px 0px 10px 0px #00FF38;  
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
        font-size: 22px;
        color: #ffc629;
        background-color: #1e1e1e;
        border-radius: 10px;
        padding: 4px 20px;
        margin-bottom: 10px;
      }
    }
  }
}
</style>
