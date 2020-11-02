<template>
    <div class="employees">
        <h1>Employees Page</h1>
        <div class="row">
            <router-link v-for="employee in employeesData"
                         :to="{name: 'Employee', params: {empID: employee.EmployeeID}}"
                         :key="employee.EmployeeID"
                         class="column">
                {{employee.FirstName}} {{employee.LastName}}
            </router-link>
        </div>
    </div>
</template>

<script>

    export default {
        name: "Employees",
        data() {
            return {
                employeesData: null,
                responseStatus: false
            }
        },
        methods: {
            getNorthwindEmployeesData() {

                this.responseStatus = false;

                fetch('https://services.odata.org/V3/Northwind/Northwind.svc/Employees?$format=json', {
                    'method': 'GET'
                })
                    .then(response => {
                        if (response.ok) {
                            this.responseStatus = true;
                            console.log("Northwind Employee Data Service returned status " + response.status);
                            return response.json();
                        } else {
                            alert("Northwind Employee Data Service returned status " + response.status);
                        }
                    })
                    .then(response => {
                        this.employeesData = response.value;
                    })
                    .catch(err => {
                        console.log(err);
                    });
            }

        },
        mounted() {
            this.getNorthwindEmployeesData();
        }

    }
</script>

<style scoped>
    .column {
        float: left;
        width: 32.2%;
        padding: 0 10px;
        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
    }

    .column:hover{
        box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
    }

    .row {
        margin: 0 -5px;
    }

    .row:after {
        content: "";
        display: table;
        clear: both;
    }

    @media screen and (max-width: 600px) {
        .column {
            width: 100%;
            display: block;
            margin-bottom: 20px;
        }
    }
</style>