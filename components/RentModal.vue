<!--utilized from - https://bootstrap-vue.org/docs/components/modal#using-show-hide-and-toggle-component-methods -->
<!-- this component demonstarated importing from plugins and libraries -->
<!-- steps:
 1. npm install v-calendar
 2. go to plugins folder and add vue-calendar.js (in this case we can just copy from v-calendar documentation)
 3. add the file path to plugins in nuxt.config.js
  -->
  <template>
    <div>
      <b-button id="show-btn" @click="showModal">Rent</b-button>
  
      <b-modal ref="myModal" hide-footer title="Using Component Methods">
        <div class="calendar-container">
          <div class="text-container">
            <p>This model takes the selected dates and the product id to than use a mutation to add this item found by id and dates to the state</p>
            <p>Than it will be rendered in My Items page</p>
          </div>
        </div>
        <div >
          <vc-date-picker 
            v-model="selectedDates" 
            color="indigo"
            is-dark
            style="margin-left: 22%"
            is-range
            @input="handleDateChange" 
          />
          <p>Start Date: {{ formatDate(selectedDates.start) }}</p>
          <p>End Date: {{ formatDate(selectedDates.end) }}</p>
        </div>
        <b-button class="mt-3" variant="outline-danger" block @click="orderItem">Order</b-button>
      </b-modal>
    </div>
  </template>
  
  <script>
  import { mapMutations } from "vuex";
  
  export default {
    props: ['product'],
    data() {
      return {
        selectedDates: {
          start: null,
          end: null
        }
      };
    },
    methods: {
      showModal() {
        this.$refs.myModal.show();
      },
      hideModal() {
        this.$refs.myModal.hide();
      },
      handleDateChange(dates) {
        this.selectedDates = dates;
      },
      formatDate(date) {
        if (!date) return '';
  
        const options = { 
          weekday: 'short', 
          year: 'numeric', 
          month: 'short', 
          day: 'numeric', 
          hour: '2-digit', 
          minute: '2-digit', 
          second: '2-digit'
        };
  
        // Create a new Date object
        const d = new Date(date);
  
        // Format date to 'Mon Aug 05 2024 16:08:44'
        return d.toLocaleString('en-US', options).replace(',', '');
      },
      orderItem() {
        // Assuming addItem expects product ID, start date, and end date
        if (this.selectedDates.start && this.selectedDates.end) {
          this.addItem({ 
            id: this.product.id, 
            from: String(this.formatDate(this.selectedDates.start)),
            untill: String(this.formatDate(this.selectedDates.end))
          });
          this.hideModal();
        } else {
          alert('Please select both start and end dates.');
        }
      },
      ...mapMutations(['addItem']),
    }
  };
  </script>
  


<style scoped>
    button {
        width: 100%;
        border: none;
        padding: 0.5rem;
        color: white;
        font-weight: 700;
        padding: 1rem 4rem;
        border-radius: 100rem;
        background-color: rgb(231, 81, 43);
        color: white;
        font-weight: 700;
        transition: 0.5s;
    }
    .calendar-container {
      margin: 0 auto;
      display: flex;
      justify-content: space-between;
    }
    p {
      color: grey
    }
    .text-container {
      padding: 0.5rem
    }
</style>

