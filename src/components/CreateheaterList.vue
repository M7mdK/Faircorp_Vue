<template>
    <div class="create border border-secondary rounded shadow-sm p-2 mb-2 mt-4 bg-white expanded">
        <div class="top-row d-flex">
            <div class="create-heater fw-bold pe-3">Create New Heater</div>
        </div>
        <hr/>
        <template>
            <form>
            <input type="text" class="form-control form-control mb-2" v-model="heaterName">
            
                <div v-for="room in rooms" v-bind:room="room" v-bind:key="room.id"  class="form-check">
                    <label class="form-check-label">
                        <input type="radio" class="form-check-input" name="roomOption" v-bind:value="room.id" v-model="roomNumber">{{room.name}}
                    </label>
                </div>

            <div class="details d-flex">
                <button type="button" class="addHeater btn p-2 btn-primary me-2" v-on:click="createHeater" v-bind:disabled="!heaterName || !roomNumber">Create Heater</button>
            </div>
            </form>
        </template>
    </div>
</template>

<script>
import axios from 'axios';
import { API_HOST } from '../config';

export default {
    name: 'CreateheaterList',
    data(){
        return {
            rooms: [],
            roomNumber: null,
            heaterName: null,
        }
    },
    
    created: async function(){
            let response = await axios.get(`${API_HOST}/api/rooms`);
            this.rooms = response.data;
    },
    methods:{
        async createHeater(){
            let postData = {
                "name": this.heaterName, 
                "roomId":this.roomNumber ,
                "heaterStatus": "OFF"
            };
            await axios.post(`${API_HOST}/api/heaters`, postData);
            location.reload()
        },
    }
}
</script>


<style lang="scss" scoped>
.create{
    .top-row {
        cursor: pointer;
    }
}
.addHeater.btn, .addHeater.btn:active{
    color: #ffffff;
    background-color: #0000ff;
}
.create {
    .top-row {
        cursor: pointer;
    }
}
</style>



