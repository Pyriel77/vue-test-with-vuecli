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
            {{ currentEvent.name.toUpperCase() }}
          </div>
          <div class="event-date">
            {{ formatDate(currentEvent.from) }} -
            {{ formatDate(currentEvent.to) }}
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
      formattedDate: '',
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
      this.overlayVisible = !this.overlayVisible;
      if (this.overlayVisible) {
        const randomIndex = Math.floor(Math.random() * this.eventData.length);
        this.currentEvent = this.eventData[randomIndex];
      } else {
        this.currentEvent = {};
      }
    },
    formatDate(inputDate) {
      const months = [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December',
      ];

      const dateParts = inputDate.split('-');

      const monthIndex = parseInt(dateParts[1]) - 1;
      const day = dateParts[2];

      return `${months[monthIndex]} ${parseInt(day)}`;
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
  position: relative;
  background-color: #252525;
  border: 4px solid #fff;
  border-radius: 20px;
  text-align: center;
  vertical-align: bottom;
  height: 32%;
  width: 50%;
}

.event-name {
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  font-size: 42px;
  font-weight: 600;
  text-shadow: 3px 3px #252525;

  height: 7rem;
  margin: 7px;
}

.event-date {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #fff;
  color: #000;
  font-size: 24px;
  margin-bottom: 7px;
  height: 3rem;
  margin: 7px;
}

.talent-container {
  display: flex;
  flex-direction: row;
  align-items: center;
  width: auto;
  height: 7rem;
  margin: 7px 5px;
}

.event-talent {
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
  font-size: 36px;
  margin: 2px;
  text-shadow: 2px 2px #252525;
  width: 100%;
  height: 100%;
  text-align: center;
}

.talent-container > div:first-child {
  text-align: left;
  border-bottom-left-radius: 10px;
}

.talent-container > div:last-child {
  text-align: right;
  justify-content: center;
  border-bottom-right-radius: 10px;
}
</style>
