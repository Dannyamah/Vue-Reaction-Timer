<template>
  <div class="block container" v-if="showBlock" @click="stopTimer">
    Click Me
  </div>
</template>

<script>

export default {
props: ['delay'],

data() {
    return {
        showBlock: false,
        timer: null,
        reactionTime: 0
    }
},

methods: {
    startTimer() {
        this.timer = setInterval(() => {
            this.reactionTime += 10
        }, 10)
    },

    stopTimer() {
        clearInterval(this.timer)
        // to emit custom event to be able to access it in another component, the second argument in the emit function is the data we want to send along with the event
        this.$emit('end', this.reactionTime)
    }
},

// Mounted life cycle hook to show when data is rendered to the DOM
mounted() {
    setTimeout(() => {
        this.showBlock = true
        this.startTimer()
    }, this.delay)
},

}
</script>

<style>
.block{
    max-width: 400px;
    border-radius: 20px;
    background: #0faf87;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
}
</style>