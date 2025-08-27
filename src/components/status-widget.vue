<script>
import axios from "axios";

export default {
  data() {
    return {
      mcsrvstatAPI: "https://api.mcsrvstat.us/3/revived.club",
      serverIcon: "",
      online: false,
      version: null,
      software: null,
      port: null,
      onlinePlayers: 0,
      maxPlayers: 0,
      requestedStatus: false,
    };
  },
  methods: {
    async requestStatus() {
      try {
        const { data } = await axios.get(this.mcsrvstatAPI);
        this.requestedStatus = true;
        this.online = data.online;

        if (data.online) {
          const { version, software, port, players, icon } = data;
          this.version = version;
          this.software = software;
          this.port = port;
          this.onlinePlayers = players.online;
          this.maxPlayers = players.max;
          this.serverIcon = icon;
        }
      } catch (error) {
        console.error("Failed to fetch server status:", error);
        this.requestedStatus = true;
      }
    },
  },
  mounted() {
    this.requestStatus();
  },
};
</script>


<template>
  <div v-if="requestedStatus" class="container">
    <div class="status-container">
      <img v-if="online" :src="serverIcon" alt="Server Icon">
      <h3 class="header">Status</h3>
      <div class="online" v-if="online">Online</div>
      <div class="offline" v-else>Offline</div>
      <div class="server-meta">
        <p v-if="version">Version: {{ this.version }}</p>
        <p v-if="software">Software: {{ this.software }}</p>
        <p v-if="port">Port: {{ this.port }}</p>
      </div>
      <p v-if="maxPlayers">{{ onlinePlayers }}/{{ maxPlayers }} Players Online</p>
      <p v-if="!online">The Server is currently offline!</p>
    </div>
  </div>

  <p class="additional-info"><span style="color: red">*</span>Status updates may take up to 5 minutes. Thank you for your patience.</p>

</template>