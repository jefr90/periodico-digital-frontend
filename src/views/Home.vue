<template>
  <div class="home">
    <h1 class="text-xl font-bold bg-gray-100 py-2">Periódico Digital</h1>
    <div class="flex mt-2 row gap-3 justify-center items-baseline">
      <div class="flex items-center bg-red-400 p-1 rounded gap-1">
        <input
          type="checkbox"
          id="internacionales"
          value="1"
          @change="toggleConnection1"
        />
        <label for="internacionales" class="font-semibold"
          >Internacionales</label
        >
      </div>
      <div class="flex items-center bg-yellow-200 p-1 rounded gap-1">
        <input
          type="checkbox"
          id="nacionales"
          value="2"
          @change="toggleConnection2"
        />
        <label for="nacionales" class="font-semibold">Nacionales</label>
      </div>
      <div class="flex items-center bg-green-200 p-1 rounded gap-1">
        <input
          type="checkbox"
          id="regionales"
          value="3"
          @change="toggleConnection3"
        />
        <label for="regionales" class="font-semibold">Regionales</label>
      </div>
    </div>

    <NewsList v-if="this.news.length" :news="this.news"></NewsList>
    <template v-else class="flex justify-center">
      <h1 class="text-lg font-semibold mt-5">
        ¡Bienvenid@! <br />Utiliza el seleccionador de tópicos para empezar a
        ver Noticias 😁
      </h1>
      <div class="max-w-md flex justify-center mx-auto">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          className="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            strokeWidth="{2}"
            d="M19 20H5a2 2 0 01-2-2V6a2 2 0 012-2h10a2 2 0 012 2v1m2 13a2 2 0 01-2-2V7m2 13a2 2 0 002-2V9a2 2 0 00-2-2h-2m-4-3H9M7 16h6M7 8h6v4H7V8z"
          />
        </svg>
      </div>
    </template>
  </div>

  <Modal v-show="isModalVisible" @close="closeModal" />
</template>

<script>
// @ is an alias to /src
import NewsList from "../components/NewsList";
import Modal from "../components/Modal.vue";

export default {
  name: "Home",
  data: function () {
    return {
      connection1: null,
      connection2: null,
      connection3: null,
      connectionDefensor: null,
      news: [],
      isModalVisible: true,
    };
  },
  components: { Modal, NewsList },
  created() {
    this.connectionDefensor = new WebSocket("ws://localhost:3000/4");
    this.connectionDefensor.onopen = function (event) {
      console.log(`WS4 connection is open`, event);
      this.isModalVisible = true;
    };
  },
  methods: {
    toggleConnection1: function () {
      if (!this.connection1) {
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
              this.news.unshift(JSON.parse(event.data));
            } catch {
              console.log("Error adding to news 1");
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
      } else {
        this.connection1.close();
        this.connection1 = null;
      }
    },
    toggleConnection2: function () {
      if (!this.connection2) {
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
              this.news.unshift(JSON.parse(event.data));
            } catch {
              console.log("Error adding to news 2");
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
      } else {
        this.connection2.close();
        this.connection2 = null;
      }
    },
    toggleConnection3: function () {
      if (!this.connection3) {
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
              this.news.unshift(JSON.parse(event.data));
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
      } else {
        this.connection3.close();
        this.connection3 = null;
      }
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      console.log("closeModal");
      this.isModalVisible = false;
    },
  },
};
</script>
