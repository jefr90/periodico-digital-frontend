<template>
  <div class="home">
    <p>Este es el home</p>
    <NewsList :news="this.news"></NewsList>
  </div>
</template>

<script>
// @ is an alias to /src
import NewsList from "../components/NewsList";

export default {
  name: "Home",
  data: function () {
    return {
      connection1: null,
      connection2: null,
      connection3: null,
      news: [],
    };
  },
  components: { NewsList },
  created() {
    console.log("Starting connection to WebSocket Server 1");

    this.connection1 = new WebSocket("ws://localhost:3000/1");

    //let serverIsOpen = true;
    this.connection1.onmessage = async (event) => {
      if (event.data instanceof Blob) {
        let reader = new FileReader();

        reader.onload = () => {
          console.log("Result: " + reader.result);
        };

        reader.readAsText(event.data);
      } else {
        console.log("Result: " + event.data);
        try {
          this.news.push(JSON.parse(event.data));
        } catch {
          console.log("Error adding to news 3");
        }
      }
    };

    this.connection1.onopen = function (event) {
      console.log(`WS1 connection is open`, event);
    };

    this.connection1.onerror = function (event) {
      console.log("Error from socket ", event);
    };

    this.connection1.onclose = function (event) {
      console.log("Websocket closed", event);
    };

    console.log("Starting connection to WebSocket Server 2");

    this.connection2 = new WebSocket("ws://localhost:3000/2");

    //let serverIsOpen = true;
    this.connection2.onmessage = async (event) => {
      if (event.data instanceof Blob) {
        let reader = new FileReader();

        reader.onload = () => {
          console.log("Result: " + reader.result);
        };

        reader.readAsText(event.data);
      } else {
        console.log("Result: " + event.data);
        try {
          this.news.push(JSON.parse(event.data));
        } catch {
          console.log("Error adding to news 3");
        }
      }
    };

    this.connection2.onopen = function (event) {
      console.log(`WS2 connection is open`, event);
    };

    this.connection2.onerror = function (event) {
      console.log("Error from socket ", event);
    };

    this.connection2.onclose = function (event) {
      console.log("Websocket closed", event);
    };

    console.log("Starting connection to WebSocket Server 3");

    this.connection3 = new WebSocket("ws://localhost:3000/3");

    //let serverIsOpen = true;
    this.connection3.onmessage = async (event) => {
      if (event.data instanceof Blob) {
        let reader = new FileReader();

        reader.onload = () => {
          console.log("Resultt: " + reader.result);
        };

        reader.readAsText(event.data);
      } else {
        console.log("Result: " + event.data);
        try {
          this.news.push(JSON.parse(event.data));
        } catch {
          console.log("Error adding to news 3");
        }
      }
    };

    this.connection3.onopen = function (event) {
      console.log(`WS3 connection is open`, event);
    };

    this.connection3.onerror = function (event) {
      console.log("Error from socket ", event);
    };

    this.connection3.onclose = function (event) {
      console.log("Websocket closed", event);
    };
  },
};
</script>
