<template>
  <div>
    <v-container grid-list-md>
      <v-layout row wrap>
        <admin-stats-card
          icon="groups"
          color="brown"
          :value="usersCount"
          unit=" users"
          label="User accounts"
          label_sub="Groups"
          :value_sub="groupsCount"
        ></admin-stats-card>
        <admin-stats-card
          icon="layers"
          color="purple"
          :value="machines"
          unit=" units"
          label="Instances"
          label_sub="Running"
          :value_sub="runningMachines"
        ></admin-stats-card>
      </v-layout>
   </v-container>
    <v-container grid-list-md>
      <v-layout row wrap>
        <host-stats-card
          icon="data_usage"
          color="green"
          :value="totalCpu"
          unit=" cores"
          label="Host CPU"
          :value_sub="vcpus"
          unit_sub=" cores"
          label_sub="Allocated CPUs"
        ></host-stats-card>
        <host-stats-card
          icon="memory"
          color="blue"
          :value="totalMemory"
          unit=" "
          label="Total Memory"
          :value_sub="memory"
          unit_sub=" GB"
          label_sub="Allocated Memory"
        ></host-stats-card>
        <host-stats-card
          icon="storage"
          color="orange"
          :value="totalDisk"
          unit=" GB"
          label="Total Disk"
          :value_sub="disk"
          unit_sub=" GB"
          label_sub="Allocated Disk"
        ></host-stats-card>
      </v-layout>
   </v-container>
  </div>
</template>

<script>
  import AdminStatsCard from './AdminStatsCard';
  import HostStatsCard from './HostStatsCard';
  import { humanFileSize } from '../../libraries/utils/helpers';
  // import Host from '../../libraries/store/modules/host';

  export default {
    name: 'AdminStats',
    components: {
      'admin-stats-card': AdminStatsCard,
      'host-stats-card': HostStatsCard
    },
    computed: {
      loading() {
        return this.$store.state.loading;
      },
      usersCount() {
        return this.$store.getters.usersTableData.length;
      },
      groupsCount() {
        return this.$store.getters.groupsTableData.length;
      },
      stats() {
        // console.log(this.$store.getters.host);
        return this.$store.getters.stats;
      },
      host() {
        return this.$store.getters.host;
      },
      machines() {
        return this.stats.containers && this.stats.containers.count;
      },
      runningMachines() {
        return this.stats.containers && this.stats.containers.count_running;
      },
      vcpus() {
        return this.stats.cpus && this.stats.cpus.cpus_count;
      },
      memory() {
        return this.stats.memory && this.stats.memory.memory_count;
      },
      disk() {
        return this.stats.disk && this.stats.disk.disk_count;
      },
      totalCpu() {
        return this.host.cpu && this.host.cpu.total;
      },
      totalMemory() {
        return this.host.memory && humanFileSize(this.host.memory.total);
      },
      totalDisk() {
        return this.host.pool && this.host.pool.space.total;
      }
    },
    mounted() {
      // console.log(this.$store.getters.stats);
      // console.log(this.$store.getters['auth/me']);
    },
    created() {
      // this.$store.registerModule('host', Host);
      this.$store.dispatch('fetchStats');
      this.$store.dispatch('fetchUsers');
      this.$store.dispatch('fetchHost');
    }
  };
</script>
