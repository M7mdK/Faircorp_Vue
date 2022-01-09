<template>
  <div class="heaters-list pt-3">
    <heaters-list-item 
      v-for="heater in heaters"
      :heater="heater"
      :key="heater.id"  
      @heater-updated="updateheater"
    >
    </heaters-list-item>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';
import heatersListItem from './HeatersListItem';

export default {
  components: {
    heatersListItem
  },
  name: 'heatersList',
  data: function() {
    return {
      heaters: []
    }
  },
  created: async function() {
    let response = await axios.get(`${API_HOST}/api/heaters`);
    let heaters = response.data;
    this.heaters = heaters;
  },
  methods: {
    updateheater(newheater) {
      let index = this.heaters.findIndex(heater => heater.id === newheater.id);
      this.heaters.splice(index, 1, newheater);
    }
  }
}
</script>