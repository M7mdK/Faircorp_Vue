<template>
  <div class="room border border-secondary rounded shadow-sm p-2 mb-2 bg-white" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="room-name fw-bold pe-3">{{room.name}}</div>
      <div class="room-floor text-muted">floor&#35;{{room.floor}}</div>
      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="details d-flex justify-content-around m-10">
        <div class="p-2">Current Temperature: {{room.currentTemperature}} &#x2103;</div>
        <div class="p-2">Target Temperature: {{room.targetTemperature}} &#x2103;</div>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: 'RoomsListItem',
  props: ['room'],
  data() {
    return {
      isExpanded: false,
      isShow: false,
      currentTemp: 0,
      targetTemp: 0,
    }
  }, 
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded;
    },
    showWindows(){
      this.isShow = !this.isShow;
      alert(this.room.name)
    },
  }
}
</script>

<style lang="scss" scoped>

.open-status {
  .icon {
    position: relative;
  }
  &.open {
    color: #00ff00;
    .icon {
      font-size: 12px;
      top: -3px;
    }
  }
  &.closed {
    color: #ff0000;
  }
}
.room {
  .top-row {
    cursor: pointer;
  }
}
.details>.p-2{
  background-color: #ff0000;
  color: #ffffff;
  border-radius: 0.25em;
}
</style>
