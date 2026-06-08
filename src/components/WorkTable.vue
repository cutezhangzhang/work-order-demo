<template>
  <a-table
    :columns="columns"
    :data-source="tableData"
    :pagination="false"
    rowKey="id"
  >
    <template #bodyCell="{ column, record }">

      <template v-if="column.dataIndex === 'overtime'">
        {{ record.overtime ? 'Yes' : 'No' }}
      </template>

      <template v-if="column.dataIndex === 'action'">
        <a-popconfirm
          title="Are you sure delete?"
          @confirm="handleDelete(record.id)"
        >
          <a-button danger size="small">
            Delete
          </a-button>
        </a-popconfirm>
      </template>

    </template>
  </a-table>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  tableData: Array,
  role: String
})

const emit = defineEmits(['delete'])

const handleDelete = (id) => {
  emit('delete', id)
}

const columns = computed(() => {
  const baseColumns = [
    {
      title: 'ID',
      dataIndex: 'id'
    },
    {
      title: 'Project',
      dataIndex: 'project'
    },
    {
      title: 'Overtime',
      dataIndex: 'overtime'
    },
    {
      title: 'Hours',
      dataIndex: 'hours'
    },
    {
      title: 'Created At',
      dataIndex: 'created_at'
    }
  ]

  if (props.role === 'admin') {
    baseColumns.push({
      title: 'Action',
      dataIndex: 'action'
    })
  }

  return baseColumns
})
</script>