<template>
  <div id="app">
    <div class="overlay">
      <button @click="toggleOverlay" class="toggle-button">
        Toggle Overlay
      </button>
      <div v-if="overlayVisible" class="overlay-content">
        <div class="event-details">
          <div
            class="event-name"
            :style="{ backgroundColor: currentEvent.color }"
          >
            {{ currentEvent.name }}
          </div>
          <div class="event-date">
            {{ currentEvent.from }} - {{ currentEvent.to }}
          </div>
          <div class="talent-container">
            <div
              v-for="(talent, index) in currentEvent.talent"
              :key="index"
              class="event-talent"
              :style="{ backgroundColor: currentEvent.color }"
            >
              {{ talent }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      overlayVisible: false,
      currentEvent: {},
      eventData: [
        {
          name: 'FGC',
          from: '2020-03-10',
          to: '2020-03-12',
          color: '#00d487',
          talent: ['LD'],
        },
        {
          name: 'Rocket League Showdown 2020 Summer Shuffle',
          from: '2020-06-29',
          to: '2020-07-12',
          color: '#e5043b',
          talent: ['EterNaLeNvy', 'DakotaCox', 'Sarah Jessica Parker'],
        },
        {
          name: 'Dota Summit',
          from: '2020-11-02',
          to: '2020-11-07',
          color: '#ca6412',
          talent: ['HMW', 'Phil'],
        },
      ],
    };
  },
  methods: {
    toggleOverlay() {
      console.log(this.overlayVisible);
      this.overlayVisible = !this.overlayVisible;
      if (this.overlayVisible) {
        const randomIndex = Math.floor(Math.random() * this.eventData.length);
        this.currentEvent = this.eventData[randomIndex];
      } else {
        this.currentEvent = {};
      }
    },
  },
};
</script>

<style lang="scss">
.toggle-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: #333;
  color: #fff;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
}

.toggle-button:hover {
  background-color: #555;
}

.overlay {
  /*display: none;*/
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #252525;
  z-index: 1000;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.overlay-content {
  width: 1920px;
  height: 950px;
  background-color: #252525;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

canvas {
  width: 100%;
  height: 50%;
}

.event-details {
  background-color: #252525;
  border: 2px solid #fff;
  border-radius: 10px;
  text-align: center;
  padding: 3px;
}

.event-name {
  color: #fff;
  border-top-right-radius: 5px;
  border-top-left-radius: 5px;
  font-size: 36px;
  font-weight: 200;
  text-shadow: 2px 2px #252525;
  margin-bottom: 10px;
}

.event-date {
  background-color: #fff;
  color: #000;
  font-size: 24px;
  margin-bottom: 10px;
}

.talent-container {
  display: flex;
  flex-direction: row;
  align-items: center;
}

.event-talent {
  color: #fff;
  font-size: 20px;
  margin: 2px;
  display: flex;
  gap: 10px;
  text-shadow: 2px 2px #252525;
}

.talent-container > div:first-child {
  text-align: left;
  border-bottom-left-radius: 5px;
}

.talent-container > div:last-child {
  text-align: right;
  border-bottom-right-radius: 5px;
}
</style>
