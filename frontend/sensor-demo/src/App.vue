<script>
import axios from 'axios'
export default{
  data() {
    return {
      sensors:[]
    }
  },
  mounted(){
    this.getAllSensors()
  },
  methods:{
    async getAllSensors(){
      const res = await axios.get('https://chenxyzj-turbo-robot-p76rrgjjpx92v95-8000.preview.app.github.dev/api/sensors')
      this.sensors = res.data
    },
    async deleteOneSensor(sensor){
      const res = await axios.delete(`https://chenxyzj-turbo-robot-p76rrgjjpx92v95-8000.preview.app.github.dev/api/sensors/${sensor.id}`)
      this.getAllSensors();
    },
    async addOneSensor(){
      await axios.post('https://chenxyzj-turbo-robot-p76rrgjjpx92v95-8000.preview.app.github.dev/api/sensors',
      {
        name: "Sensor New"
      })      

      this.getAllSensors();
    }
  }
}
</script>

<template>
  <button @click="getAllSensors">Get All Sensors</button>
  <button @click="addOneSensor">Add One Sensor</button>
  <ul>
    <li v-for="sensor in sensors">
      {{sensor.id}} - {{sensor.name}}
      <button @click="deleteOneSensor(sensor)">x</button>
    </li>
  </ul>
</template>

<style scoped>

</style>
