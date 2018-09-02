<template>
  <div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      params: {
        statrTime: '',
        endTime: ''
      }
    }
  },
  computed: {
    time: {
      get () {
        return `${this.statrTime}-${this.endTime}`
      },
      set (val) {
        const time = val.split('-') || []
        this.params.statrTime = time[0]
        this.params.endTime = time[1]
      }
    }
  }
}
</script>
