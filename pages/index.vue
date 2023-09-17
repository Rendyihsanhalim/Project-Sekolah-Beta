<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom d-flex align-items-center justify-content-between py-2">
        <h5>Task</h5>
        <div class="d-flex align-items-center">
          <input type="text" class="form-control" placeholder="Search" v-model="searchQuery">
          <div class="d-flex align-item-center justify-content-end w-100">
            <span class="me-2">View As</span>
            <button class="btn btn-outline-secondary py-1 px-3" @click="isGrid = !isGrid">
              {{ isGrid ? 'Grid' : 'List' }}
            </button>
          </div>
        </div>
      </div>
      <div class="list-task row">
        <CardItem v-for="(task, i) in resultQuery" :key="i" :task="task" :isGrid="isGrid" />
      </div>
      <form v-on:submit.prevent="handleSubmit">
        <div class="action py-2">
          <a v-if="!isCreating" href="#" class="add-button" @click="isCreating = !isCreating">Add Task</a>
          <div v-else class="add-card">
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input v-model="form.title" class="form-control border-0 mb-2" placeholder="Title" type="text">
                <textarea v-model="form.description" class="form-control border-0 small" placeholder="Description"
                  rows="3"></textarea>
              </div>
            </div>
            <div class="button-wrapper d-flex">
              <button class="btn btn-primary me-2">Save</button>
              <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue"
export default {
  layout(context) {
    return 'custom'
  },
  components: {
    CardItem
  },
  data() {
    return {
      searchQuery: '',
      // Tipe layout daftar task
      isGrid: true,
      // Status saat menambahkan task
      isCreating: false,
      // Daftar task
      tasks: [
        {
          title: 'Task 1',
          description: 'ini deskripsi 1',
          isDone: false,
        },
        {
          title: 'Tugas 2',
          description: 'ini deskripsi 2',
          isDone: false,
        },
        {
          title: 'Kerja 3',
          description: 'ini deskripsi 3',
          isDone: false,
        },
      ],
      form: {
        title: "",
        description: "",
        isDone: false,
      },
    }
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.tasks.filter((item) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => item.title.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks)
        return this.tasks
      }
    }
  },

  methods: {
    handleSubmit() {
      const newTask = {
        title: this.form.title,
        description: this.form.description,
        isDone: false,
      };

      this.tasks.push(newTask);

      // Untuk Mereset agar di tampilan menjadi kosong
      this.form.title = "";
      this.form.description = "";

    },
  },

}
</script>
<style></style>