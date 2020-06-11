<template>
  <div>
    <div id="vue-root">
      <datatable :data="shipments"></datatable>
    </div>
    <table>
      <tr v-for="(item, index) in shipments" :key="index">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>

        <td>
          <span v-for="(good, i) in item.cargo" :key="i">
            <small style="color:red;">Type: {{ good.type }}</small> |
            <small style="color:green;">Description: {{ good.description }}</small>
            |
            <small style="color:blue;">Volume: {{ good.volume }}</small> |
          </span>
        </td>
        <td>{{ item.mode}}</td>
        <td>{{ item.destination}}</td>
        <td>{{ item.origin}}</td>
        <td>
          <span v-for="(serve, s) in item.service " :key="s">
            <small class="text-danger">{{ serve.type }}</small>
            <small class="text-info">{{ serve.value }}</small>
          </span>
        </td>
        <td>{{ item.total}}</td>
        <td>{{ item.status}}</td>
        <td>{{ item.userId}}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import json from "../../db.json";
export default {
  name: "Shipment",
  data() {
    return {
      shipments: json
    };
  },
  created() {
    this.getShipment();

    console.log(this.shipments);
  },
  methods: {
    getShipment() {
      fetch("http://localhost:3000/shipments")
        .then(response => response.json())
        .then(data => (this.shipments = data));
    }
  }
};
</script>
