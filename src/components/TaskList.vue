<!-- TaskList.vue -->
<template>
  <div class="app">
    <h1>Daftar Kegiatan</h1>
    <div class="input-container">
      <input v-model="newActivity" placeholder="Tambah kegiatan baru">
      <button @click="addActivity">Tambah</button>
    </div>
    <div>
      <button @click="showIncomplete = false">Tampilkan semua</button>
      <button @click="showIncomplete = true">filter</button>
    </div>
    <ul>
      <li v-for="(activity, index) in filteredActivities" :key="index">
        <input type="checkbox" v-model="activity.completed">
        <span :class="{ 'completed': activity.completed }">{{ activity.name }}</span>
        <button @click="cancelActivity(index)">Batalkan</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newActivity: '',
      activities: [],
      showIncomplete: false
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity.trim() !== '') {
        this.activities.push({ name: this.newActivity, completed: false });
        this.newActivity = '';
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1);
    }
  },
  computed: {
    filteredActivities() {
      if (this.showIncomplete) {
        return this.activities.filter(activity => activity.completed);
      } else {
        return this.activities;
      }
    }
  }
};
</script>

<style scoped>
.completed {
  text-decoration: line-through;
}
</style>
