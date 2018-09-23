<template>
  <div class="container main">
    <section class="is-large">
      <Notification v-if="success"></Notification>
      <ProgressBar v-if="percentage" :success="success" :percentage="percentage"></ProgressBar>
      <div class="columns">
        <CompanyCard v-on:caps="caps" v-for="company in companies" :element="company" :key="company.id"></CompanyCard>
      </div>
    </section>
  </div>
</template>

<script type="text/javascript">
  import CompanyCard from './CompanyCard.vue'
  import ProgressBar from './ProgressBar.vue'
  import Notification from './Notification.vue'

  export default {
    name: 'maincontent',
    data () {
      return {
        companies: [
          {id: 1776},
          {id: 1758}
        ],
        percentage: null,
        cache: null,
        success: false
      }
    },
    components: {
      CompanyCard,
      ProgressBar,
      Notification
    },
    methods: {
      caps (value) {
        if (this.cache) {
          if (this.cache[0] == 1758) {
            this.percentage = value[1]/this.cache[1]*100
          } else {
            this.percentage = this.cache[1]/value[1]*100 
          }
          this.$emit('setChangedStatus','isLoaded');
          if (this.percentage > 100) {
            this.success = true;
            this.$emit('setChangedStatus','success')
          }
        } else {
          this.cache = value;
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  .main {
    @media screen and (max-width: 1090px) {
      padding: 0 1.5rem;
    }
  }
</style>