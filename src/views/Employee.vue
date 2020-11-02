<template>
    <div class="employee">
        <h1>Employee Details Page</h1>
        <div class="details">
            <table>
                <tr>
                    <th>EmployeeID</th>
                    <td>{{employee.EmployeeID}}</td>
                </tr>
                <tr>
                    <th>FirstName</th>
                    <td>{{employee.FirstName}}</td>
                </tr>
                <tr>
                    <th>Title</th>
                    <td>{{employee.Title}}</td>
                </tr>
                <tr>
                    <th>TitleOfCourtesy</th>
                    <td>{{employee.TitleOfCourtesy}}</td>
                </tr>
                <tr>
                    <th>BirthDate</th>
                    <td>{{employee.BirthDate}}</td>
                </tr>
                <tr>
                    <th>HireDate</th>
                    <td>{{employee.HireDate}}</td>
                </tr>
                <tr>
                    <th>Address</th>
                    <td>{{employee.Address}}</td>
                </tr>
                <tr>
                    <th>City</th>
                    <td>{{employee.City}}</td>
                </tr>
                <tr>
                    <th>Region</th>
                    <td>{{employee.Region}}</td>
                </tr>
                <tr>
                    <th>PostalCode</th>
                    <td>{{employee.PostalCode}}</td>
                </tr>
                <tr>
                    <th>Country</th>
                    <td>{{employee.Country}}</td>
                </tr>
                <tr>
                    <th>HomePhone</th>
                    <td>{{employee.HomePhone}}</td>
                </tr>
                <tr>
                    <th>Extension</th>
                    <td>{{employee.Extension}}</td>
                </tr>
                <tr>
                    <th>Notes</th>
                    <td>{{employee.Notes}}</td>
                </tr>
                <tr>
                    <th>ReportsTo</th>
                    <td>{{employee.ReportsTo}}</td>
                </tr>
                <tr>
                    <th>PhotoPath</th>
                    <td>{{employee.PhotoPath}}</td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
    import {useRoute} from 'vue-router';

    export default {
        name: "Employee",
        data() {
            return {
                empID: useRoute().params.empID,
                employee: null,
                responseStatus: false
            }
        },
        created() {

            this.responseStatus = false;

            fetch('https://services.odata.org/V3/Northwind/Northwind.svc/Employees?$filter=EmployeeID%20eq%20' + this.empID + '&$format=json', {
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
                    this.employee = response.value[0];
                })
                .catch(err => {
                    console.log(err);
                });
        }
    }
</script>

<style scoped>
    table {
        width: 100%;
        border: 1px solid black;
    }

    th {
        background-color: lightgrey;
    }

    th, td {

        text-align: left;
    }

</style>