<template>
  <q-page padding>
    <!-- content -->
    <h5>User management page</h5>
    <div class="q-pa-md">
      <q-table title="Treats" :rows="rows" :columns="columns" row-key="id" :filter="filter" :loading="loading">

        <template v-slot:top>
          <q-btn color="primary" :disable="loading" label="Add User" @click="addRow" />
          <!-- <q-btn class="q-ml-sm" color="primary" :disable="loading" label="Remove row" @click="removeRow" /> -->
          <q-space />
          <q-input borderless dense debounce="300" color="primary" v-model="filter">
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

      </q-table>
    </div>
  </q-page>
</template>

<script lang="ts">
import { ref } from 'vue'

const columns = [
  {
    name: 'id',
    required: true,
    label: 'id',
    align: 'left',
    field: row => row.id,
    format: val => `${val}`,
    sortable: true
  },
  { name: 'name', align: 'left', label: 'username', field: 'name', sortable: true },
  { name: 'email', label: 'email', field: 'email', sortable: true },
  { name: 'status', label: 'status', field: 'status' },
  { name: 'delete', label: 'delete user', field: 'delete' },
]

const originalRows = [
  {
    name: 'Frozen Yogurt',
    id: 159,
    email: 6.0,
    status: 24,
    delete: 4.0,
  },
  {
    name: 'Ice cream sandwich',
    id: 237,
    email: 9.0,
    status: 37,
    delete: 4.3,
  },
  {
    name: 'Eclair',
    id: 262,
    email: 16.0,
    status: 23,
    delete: 6.0,
  },
]

export default {
  setup() {
    const loading = ref(false)
    const filter = ref('')
    const rowCount = ref(10)
    const rows = ref([...originalRows])

    return {
      columns,
      rows,

      loading,
      filter,
      rowCount,

      // emulate fetching data from server
      addRow() {
        loading.value = true
        setTimeout(() => {
          const
            index = Math.floor(Math.random() * (rows.value.length + 1)),
            row = originalRows[Math.floor(Math.random() * originalRows.length)]

          if (rows.value.length === 0) {
            rowCount.value = 0
          }

          row.id = ++rowCount.value
          const newRow = { ...row } // extend({}, row, { name: `${row.name} (${row.__count})` })
          rows.value = [...rows.value.slice(0, index), newRow, ...rows.value.slice(index)]
          loading.value = false
        }, 500)
      },

      removeRow() {
        loading.value = true
        setTimeout(() => {
          const index = Math.floor(Math.random() * rows.value.length)
          rows.value = [...rows.value.slice(0, index), ...rows.value.slice(index + 1)]
          loading.value = false
        }, 500)
      }
    }
  }
}
</script>
