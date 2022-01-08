<template>
    <div class="create border border-secondary rounded shadow-sm p-2 mb-2 mt-4 bg-white expanded">
        <div class="top-row d-flex">
            <div class="create-window fw-bold pe-3">Create New Window</div>
        </div>
        <hr/>
        <template>
            <form>
            <input type="text" class="form-control form-control mb-2" v-model="windowName">

            
                <div v-for="room in rooms" v-bind:room="room" v-bind:key="room.id"  class="form-check">
                    <label class="form-check-label">
                        <input type="radio" class="form-check-input" name="roomOption" v-bind:value="room.id" v-model="roomNumber">{{room.name}}
                    </label>
                </div>

            <div class="details d-flex">
                <button type="button" class="addWindow btn p-2 btn-primary me-2" v-on:click="createWindow" v-bind:disabled="!windowName || !roomNumber">Create window</button>
            </div>
            </form>
        </template>
    </div>
</template>

<script>
import axios from 'axios';
import { API_HOST } from '../config';

export default {
    name: 'CreateList',
    data(){
        return {
            rooms: [],
            roomNumber: null,
            windowName: null,
        }
    },
    
    created: async function(){
            let response = await axios.get(`${API_HOST}/api/rooms`);
            this.rooms = response.data;
    },
    methods:{
        async createWindow(){
            let postData = {
                "name": this.windowName, 
                "roomId":this.roomNumber ,
                "windowStatus": "CLOSED"
            };
            await axios.post(`${API_HOST}/api/windows`, postData);
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
.addWindow.btn, .addWindow.btn:active{
    color: #ffffff;
    background-color: #00ff00;
    border-color: #00ff00;
}
.create {
    .top-row {
        cursor: pointer;
    }
}
</style>