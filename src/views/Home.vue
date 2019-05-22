<template>
  <div class="home">
    <h1>testing</h1>
    <EmployeeForm @add:employee="addEmployee"/>
    <EmployeeTable
      @delete:employee="deleteEmployee"
      @edit:employee="editEmployee"
      :employees="employees"/>
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue';
import EmployeeForm from '@/components/EmployeeForm.vue';
import axios from 'axios';

export default {
  name: 'home',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [],
    };
  },
  created() {
    this.getEmployees();
  },
  methods: {
    async getEmployees() {
      try {
        const response = await axios('https://jsonplaceholder.typicode.com/users');
        this.employees = response.data;
      } catch (error) {
        console.log(error);
      }
    },
    async addEmployee(employee) {
      try {
        debugger;
        // employee = JSON.stringify(employee);
        const response = await axios({
          method: 'post',
          url: 'https://jsonplaceholder.typicode.com/users',
          data: JSON.stringify(employee),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },
        })
        const newEmployee = response.data;
        this.employees = [...this.employees, newEmployee];
      } catch (error) {
        console.log(error);
      }
      
    },
    deleteEmployee(id) {
      const index = this.employees.findIndex(e => e.id === id);
      this.employees.splice(index, 1);
    },
    editEmployee(id, updatedEmployee) {
      this.employees = this.employees.map((employee) => {
        return employee.id === id ? updatedEmployee : employee;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
  .home{
    max-width: 1180px;
    margin: auto;
    text-align: left;
  }
</style>
