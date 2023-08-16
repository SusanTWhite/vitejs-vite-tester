<script setup lang="ts">
import { ref } from 'vue';
const count = ref(0);
const status = 6;
const visits = ref([
  {
    visitId: 1,
    visitStatusStr: 'Cancelled',
    visitStatus: 6,
    creationUserDisplayName: 'Amy Wheeler',
  },
  {
    visitId: 2,
    visitStatusStr: 'Requested',
    visitStatus: 1,
    creationUserDisplayName: 'Lino Ortolano',
  },
  {
    visitId: 3,
    visitStatusStr: 'Declined',
    visitStatus: 4,
    creationUserDisplayName: 'Keith David',
  },
  {
    visitId: 4,
    visitStatusStr: 'Request Declined',
    visitStatus: 8,
    creationUserDisplayName: 'Zoe Saldana',
  },
]);

let actives = visits.value.filter(
  (v) => v.visitStatus === status || (v.visitStatus === 8 && status === 6)
);
defineProps<{ msg: string }>();
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <!--button type="button" @click="count++">count is {{ count }}</button-->
    <div v-for="active in actives">
      {{ active.visitStatus }}: {{ active.visitStatusStr }}
    </div>
    <!--      
      v-model:selection="selectedVisit"
      v-model:filters="filters"
      dataKey="visitId"
      @rowSelect="onRowSelect"
      :globalFilterFields="['program.name', 'visitTypeStr', 'scheduledDateStr']"
    -->
    <DataTable
      :value="actives"
      :rows="5"
      selectionMode="single"
      :paginator="true"
      :rowsPerPageOptions="[5, 20, 50]"
      currentPageReportTemplate=" {totalRecords} visits found"
      paginatorTemplate="CurrentPageReport  PrevPageLink PageLinks NextPageLink"
    >
      <Column field="visitId" :hidden="true"></Column>
      <Column
        field="visitTypeStr"
        header="Visit Type"
        :sortable="true"
      ></Column>
      <!--This column only displays on Requested visits-->
      <Column
        v-if="actives.some((v) => v.visitStatusStr === 'Requested')"
        field="creationUserDisplayName"
        header="Requested By"
        sortable
      ></Column>
      <Column
        v-if="
          actives.some(
            (v) =>
              v.visitStatusStr === 'Cancelled' ||
              v.visitStatusStr === 'Request Declined'
          )
        "
        field="visitStatusStr"
        header="Reason"
      ></Column>
    </DataTable>
    <!--p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p-->
  </div>

  <!--p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p-->
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
