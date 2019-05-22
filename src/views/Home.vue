<template>
  <div class="home">
    <h1>testing</h1>
    <EmployeeForm @add:employee="addEmployee"/>
    <EmployeeTable :employees="employees"/>
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable.vue';
import EmployeeForm from '@/components/EmployeeForm.vue';

export default {
  name: 'home',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [
        {
          id: 1,
          name: 'Richard Hendricks',
          email: 'richard@piedpiper.com',
        },
        {
          id: 2,
          name: 'Bertram Gilfoyle',
          email: 'gilfoyle@piedpiper.com',
        },
        {
          id: 3,
          name: 'Dinesh Chugtai',
          email: 'dinesh@piedpiper.com',
        },
      ],
    };
  },
  methods: {
    addEmployee(employee) {
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      this.employees = [...this.employees, newEmployee];
      console.log(this.employees);
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
