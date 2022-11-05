<template>
  <div id="app">

      <new-student-form></new-student-form>
      <student-table></student-table>
      <student-message></student-message>

  </div>
</template>

<script>
import NewStudentForm from './components/NewStudentForm.vue'
import StudentMessage from './components/StudentMessage.vue'
import StudentTable from './components/StudentTable.vue'

export default {
  name: 'App',
  components: {
    NewStudentForm,
    StudentMessage,
    StudentTable
  }
}
</script>

<style>



</style>
