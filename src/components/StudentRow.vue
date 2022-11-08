<template>
    <tr v-bind:class="{present: student.present, absent: !student.present}">
        <td>{{student.name}}</td>
        <td>{{student.starID}}</td>
        <td>
            <input type="checkbox" 
                v-bind:checked="student.checked" 
                v-on:change="arrivedOrLeft(student, $event.srcElement.checked)">
        </td>
        <td v-on:click="studentDeleted" v-show="edit">
            <img src="@/assets/delete-button-icon.png" id="delete-icon"></td>
    </tr>
</template>

<script>

export default {
    name: "StudentRow",
    props: {
        student: Object,
        edit: Boolean
    },
    methods: {
        arrivedOrLeft(student, present) {
            this.$emit('student-arrived-or-left', student, present)
        },
        studentDeleted() {
            if (confirm (`Delete ${this.student.name}?`)) {
                this.$emit('student-deleted', this.student)
            }
        }
    }
}

</script>

<style>
    .present {
        color: gray;
        font-style: italic;
    }

    .absent {
        color: black;
        font-weight: bold;
    }

    #delete-icon {
        height: 35px;
        width: auto;
    }
</style>