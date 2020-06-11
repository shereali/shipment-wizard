<template>
  <div>
    <table>
      <tr v-for="(item, index) in shipments" :key="index">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>
          <span v-for="(good, i) in item.cargo" :key="i">
            <small style="color:red;">Type: {{ good.type }}</small> |
            <small style="color:green;"
              >Description: {{ good.description }}</small
            >
            | <small style="color:blue;">Volume: {{ good.volume }}</small> |
          </span>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "Shipment",
  data() {
    return {
      shipments: []
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
