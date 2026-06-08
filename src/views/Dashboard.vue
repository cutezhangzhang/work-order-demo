<template>
  <div class="dashboard">

    <a-card>

      <div class="header">

        <h2>
          Work Order Management
        </h2>

        <div class="user-info">

          <div class="role">
            Current Role:
            <a-tag color="blue">
              {{ role }}
            </a-tag>
          </div>

          <a-button
            danger
            size="small"
            class="logout-btn"
            @click="logout"
          >
            Logout
          </a-button>

        </div>

      </div>

      <WorkTable
        :tableData="tableData"
        :role="role"
        @delete="handleDelete"
      />

      <ProjectChart
        :tableData="tableData"
      />

    </a-card>

  </div>
</template>

<script setup>
import { ref } from 'vue'

import WorkTable from '../components/WorkTable.vue'
import ProjectChart from '../components/ProjectChart.vue'

import { workOrders } from '../mock/data'

const role = localStorage.getItem('role')

const tableData = ref([...workOrders])

const handleDelete = (id) => {

  tableData.value = tableData.value.filter(
    item => item.id !== id
  )
}

const logout = () => {
  localStorage.removeItem('role')
  location.href = '/'
}
</script>

<style scoped>
.dashboard {
  padding: 40px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 24px;
}

.user-info {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
}

.role {
  margin-bottom: 6px;
}

.logout-btn {
  min-width: 70px;
}
</style>