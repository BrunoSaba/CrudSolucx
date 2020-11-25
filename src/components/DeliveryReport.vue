<template>
  <div>
    <div>
      <b-nav id="nav-sup">
        <b-container>
          <b-row>
            <h6>Drone ID</h6>
            <br />
            <h6>Name</h6>
            <br />
            <h6>Current fly</h6>
            <br />
            <h6>Status</h6>
            <br />
          </b-row>
        </b-container>
        <b-nav-form @submit.stop.prevent="alert('Form Submitted')">
          <b-form-input
            aria-label="Input"
            class="mr-4"
            v-model="search"
            placeholder="Search id"
            
          >
          </b-form-input>
          <b-form-input
            aria-label="Input"
            class="mr-4"
            v-model="search"
            placeholder="Search Name"
          >
          </b-form-input>
          <b-form-input
            aria-label="Input"
            class="mr-4"
            v-model="search"
            placeholder="Search"
          >
          </b-form-input>
          <b-form-input
            aria-label="Input"
            class="mr-4"
            v-model="search"
            placeholder="Search"
          >
          </b-form-input>
        </b-nav-form>
      </b-nav>
    </div>

    <b-table
      :per-page="perPage"
      :items="items"
      :fields="fields"
      responsive="sm"
      :current-page="currentPage"
    >
      <template #cell(name)="data">
        <b-card>
          <b-container>
            <b-row>
              <b-avatar :src="data.item.image" size="4rem"> </b-avatar>
              <slot>
                <p>
                  {{ data.item.name }}
                  <br />
                  {{ data.item.address }}
                </p>
              </slot>
            </b-row>
          </b-container>
        </b-card>
      </template>

      <template #cell(battery)="data">
        <div  v-b-tooltip.hover.v-info ="data.item.battery">
          <b-progress
            :value="data.item.battery"
            variant="info"
            :striped="striped"
            class="mt-2"
          ></b-progress>
        </div>
      </template>

      <template #cell(max_speed)="data">
        <p>{{ data.item.max_speed }}</p>
      </template>

      <template #cell(average_speed)="data">
        <p>{{ data.item.average_speed }}</p>
      </template>

      <template #cell(fly)="data">
        <div v-b-tooltip.hover.v-info ="data.item.fly">
        <b-progress
          :value="data.item.fly"  variant="info" :striped="striped" class="mt-2"
        >
        </b-progress>
        </div>
      </template>

      <template #cell(status)="data">
        <span>
          <b-button variant="outline-primary">{{ data.item.status }}</b-button>
        </span>
      </template>
    </b-table>

    <div id="pagination-inf">
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        aria-controls="my-table"
      ></b-pagination>
    </div>

  </div>
</template>

<script>
import axios from "axios";


export default {

  el: "#app",
  mounted() {
    axios.get("http://services.solucx.com.br/mock/drones/").then((response) => {
      this.items = response.data;
    });
  },

  data() {
    return {
      selectedRows: [],
      posts: [{}],
      items: [{}],
      perPage: 5,
      currentPage: 1,
      selected: [],
      fields: [
        { key: "id", label: "drone" },
        { key: "name", label: "name" },
        { key: "battery", label: "batteries" },
        { key: "max_speed", label: "max speed" },
        { key: "average_speed", label: "Average speed" },
        { key: "fly", label: "Current fly" },
        { key: "status", label: "Status" },
      ],
    };
  },
  computed: {
    rows() {
      return this.items.length;
    },
  },

};
</script>

<style>
.thead {
  color: blue;
  border-top-left-radius: 2rem;
}
.nav {
  display: flex;
  flex-wrap: wrap;
  padding-left: 0;
  margin: auto;
  justify-content: center;
}
.table {
  margin-top: 5rem;
}
h6 {
  display: flex;
  flex-wrap: wrap;
  padding-left: 0;
  margin-left: 85px;
  margin-right: 105px;
  justify-content: center;
}

.progress {
  background-color: lightblue;
  height: 100%;
  display: flex;
  justify-content: center;
}

#pagination-inf {
  display: flex;
  flex-wrap: wrap;
  padding-left: 0;
  margin: auto;
  justify-content: center;
}

p {
  text-align: left;
  margin-left: 50px;
  color: blue;
  text-transform: unset;
  letter-spacing: 1px;
}

.table {
  float: center;
}
</style>
