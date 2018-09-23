<template>
  <div class="progressBorder animated fadeInDown">
    <progress class="progress is-large is-info" :class="{'is-success': success}" :value="progress" max="100"></progress>
    <p class="subtitle has-text-centered has-text-weight-bold">
      <span class="tag is-info is-large animated fadeInUp " :class="{'is-success': success}">{{ progress.toFixed(2) }} %</span>
    </p>
  </div>
</template>

<script type="text/javascript">
  export default {
    name: 'progressbar',
    components: {

    },
    data () {
      return {
        progress: 0
      }
    },
    props: {
      percentage: {
        type: Number,
        default: 0
      },
      success: {
        type: Boolean,
        default: false
      }
    },
    mounted () {
      let interval = setInterval(() => {
        this.progress = this.progress + Math.random();
        if (this.percentage) {
          if (this.progress >= this.percentage) {
            clearInterval(interval);
            this.progress = this.percentage;
          }
        }
      }, 7)
    }
  }
</script>

<style scoped lang="scss">
  .progressBorder {
    margin: 5em 0;
  }
</style>