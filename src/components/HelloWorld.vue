<template>
  <div class="hello">
    <ul>
      <li
        v-for="event in events"
        v-bind:key="event.id"
      >{{ event.id }} - {{ event.title }} at {{ event.location.name }}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data() {
    return {
      events: []
    };
  },
  async mounted() {
    try {
      var result = await axios({
        method: "POST",
        url: "https://fakeql.com/graphql/9a7af74c7db157da149cdfd92e31902a",
        data: {
          query: `
            {
              events {
                id
                title
                location {
                  name
                }
              }
            }
          `
        }
      });
      this.events = result.data.data.events;
    } catch (error) {
      console.error(error);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
