<template>
  <div>
    <div class="container-content">
      <h2>AP-List</h2>
      <Router v-for="router in routers" :key="router.routerId" :router="router"></Router>
    </div>
  </div>
</template>

<script>
import Router from '../components/debug/DebugRouter.vue'
import DataController from '../controllers/DataController'

export default {
  components: {
    Router
  },
  data () {
    return {
      routers: [
        {
          mac: 'D1:C2:A3:4D:4d',
          lastseen: '2018-10-19T21:35:48.995053Z'
        },
        {
          mac: 'D1:C2:A3:4D:5d',
          lastseen: '2018-10-19T21:35:48.995053Z'
        },
        {
          mac: 'D1:C2:A3:4D:6d',
          lastseen: '2018-10-25T15:28:00.995053Z'
        },
        {
          mac: 'D1:C2:A3:4D:7d',
          lastseen: '2018-10-19T21:35:48.995053Z'
        },
        {
          mac: 'D1:C2:A3:4D:8d',
          lastseen: '2018-10-19T21:35:48.995053Z',
          status: false
        },
        {
          mac: 'D1:C2:A3:4D:9d',
          lastseen: '2018-10-19T21:35:48.995053Z'
        },
        {
          mac: 'D1:C2:A3:4D:10',
          lastseen: '2018-10-19T21:35:48.995053Z'
        }
      ]
    }
  },
  mounted () {
    setInterval(() => {
      this.getNewRouterDater()
    }, 5000)
    this.getNewRouterDater()
  },
  beforeMount () {
    this.controller = new DataController(this.$api)
  },
  methods: {
    getNewRouterDater () {
      this.controller.getRouterLastSeenData()
        .then(data => this.routers = data)
    }
  }
}
</script>

<style lang="less" scoped>
.clear {
  clear: both
}
h2{
  margin-left: 10px;
  margin-bottom: 20px;
}
</style>
