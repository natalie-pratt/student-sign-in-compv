<template>
  <div id="app">
      <new-student-form v-on:student-added="newStudentAdded"></new-student-form>
      <student-table 
        v-bind:students="students" 
        v-on:student-arrived-or-left="studentArrivedOrLeft"
        v-on:student-deleted="studentDeleted">
      </student-table>
      <student-message v-bind:student="mostRecentStudent"></student-message>
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
  }, 
  data() {
    return {
      students: [],
      mostRecentStudent: {}
    }
  }, 
  methods: {
    newStudentAdded(student) {
      this.students.push(student) // Add student to list of students when method is called
      this.students.sort(function(s1, s2) { // Sort students in alphabetical order case-insensitively
        return s1.name.toLowerCase() < s2.name.toLowerCase() ? -1 : 1
      })
    },
    studentArrivedOrLeft(student, present) { // When 'present' checkbox is (un)checked, child will alert parent of event
      let updateStudent = this.students.find(function(s) {
        if (s.name === student.name && s.starID === student.starID) { // Find the student in question 
          return true
        }
        })
        
        if (updateStudent) { // If student is present, change status to present
          updateStudent.present = present
          this.mostRecentStudent = updateStudent // Change most recent student to last student to check or uncheck box
        }
    }, 
    studentDeleted(student) {
        this.students = this.students.filter(function(s) {
          if(s != student) { // Return all students who do not match that of the selected student to delete
            return true
          }
        })
        
        this.mostRecentStudent = {} // Change most recent student to empty object to remove welcome/fairwell statement
      }    
  }
}
</script>

<style>

  @import "https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css";

</style>
