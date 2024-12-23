<template>
  <div class="container">
    <h3 align="center" class="mt-5">Employee Management</h3>
    <div class="row">
      <div class="col-md-10"></div>
      <div class="col-md-12">
        <div class="form-area">
          <form @submit.prevent="save" id="check-register-form">
            <div class="row">
              <div class="col-md-6">
                <label>Employee Name</label>
                <v-text-field v-model="employee.name" label="Employee Name" required></v-text-field>
              </div>
              <div class="col-md-6">
                <label>Employee Address</label>
                <v-text-field v-model="employee.address" label="Employee Address" required></v-text-field>
              </div>
            </div>
            <div class="row">
              <div class="col-md-12">
                <label>Phone</label>
                <v-text-field v-model="employee.phone" label="Phone Number" required></v-text-field>
              </div>
            </div>
            <div class="row">
              <div class="col-md-12 mt-2">
                <v-btn type="submit" color="warning" form="check-register-form">Save</v-btn>
              </div>
            </div>
          </form>
        </div>

        <!-- Employee Table -->
        <table class="table table-dark mt-4">
          <thead>
            <tr>
              <th>Employee ID</th>
              <th>Employee Name</th>
              <th>Address</th>
              <th>Phone</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="employee in result" :key="employee.id">
              <td>{{ employee.id }}</td>
              <td>{{ employee.name }}</td>
              <td>{{ employee.address }}</td>
              <td>{{ employee.phone }}</td>
              <td>
                <v-btn type="button" color="blue" @click="edit(employee)">Edit</v-btn>
                <v-btn type="button" color="purple" @click="remove(employee)">Delete</v-btn>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Employee",
  data() {
    return {
      result: [], // Changed to an array to properly display employee data
      employee: {
        id: "",
        name: "",
        address: "",
        phone: "",
      },
    };
  },
  created() {
    this.EmployeeLoad();
  },
  methods: {
    // Load employees from the backend
    EmployeeLoad() {
      axios
        .get("http://127.0.0.1:8000/api/employee")
        .then(({ data }) => {
          this.result = data;
        })
        .catch((error) => {
          console.error("Error fetching employees:", error);
        });
    },

    // Save or update employee
    save() {
      if (this.employee.id === "") {
        this.saveData();
      } else {
        this.updateData();
      }
    },

    // Save new employee
    saveData() {
      axios
        .post("http://127.0.0.1:8000/api/employee", this.employee)
        .then(() => {
          this.EmployeeLoad();
          this.resetForm();
        })
        .catch((error) => {
          console.error("Error saving employee:", error);
        });
    },

    // Edit employee
    edit(employee) {
      this.employee = { ...employee }; // Avoid direct mutation
    },

    // Update existing employee
    updateData() {
      const editUrl = `http://127.0.0.1:8000/api/employee/${this.employee.id}`;
      axios
        .put(editUrl, this.employee)
        .then(() => {
          alert("Employee updated successfully!");
          this.EmployeeLoad();
          this.resetForm();
        })
        .catch((error) => {
          console.error("Error updating employee:", error);
        });
    },

    // Remove employee
    remove(employee) {
      const deleteUrl = `http://127.0.0.1:8000/api/employee/${employee.id}`;
      if (confirm(`Are you sure you want to delete ${employee.name}?`)) {
        axios
          .delete(deleteUrl)
          .then(() => {
            alert("Employee deleted successfully!");
            this.EmployeeLoad();
          })
          .catch((error) => {
            console.error("Error deleting employee:", error);
          });
      }
    },

    // Reset form fields
    resetForm() {
      this.employee = {
        id: "",
        name: "",
        address: "",
        phone: "",
      };
    },
  },
};
</script>

<style scoped>
.form-area {
  padding: 20px;
  margin-top: 20px;
  background-color: #0b0b0b;
  color: #ffffff;
  border-radius: 8px;
}
table {
  width: 100%;
  border-collapse: collapse;
}
table th,
table td {
  text-align: left;
  padding: 10px;
  border: 1px solid #444;
}
</style>
