<template>
    <div>
            
            <div class="container-fluid">
                <div class="row">
                    <div class="col-md-3">
                        <h1 class="mt-5 mb-5">employee</h1>
                        <b-list-group style="max-width: 300px;">
      <b-list-group-item class="d-flex align-items-center">
        <b-avatar class="mr-3"></b-avatar>
        <span class="mr-auto">Arena Sport</span>
      </b-list-group-item>
      <b-list-group-item class="d-flex align-items-center">
        <b-avatar variant="primary" text="BV" class="mr-3"></b-avatar>
        <span class="mr-auto">DSV</span>
      </b-list-group-item>
      <b-list-group-item class="d-flex align-items-center">
        <b-avatar variant="info" text="SM" class="mr-3"></b-avatar>
        <span class="mr-auto">Seafood Mall</span>
      </b-list-group-item>
      <b-list-group-item class="d-flex align-items-center">
        <b-avatar variant="success" icon="people-fill" class="mr-3"></b-avatar>
        <span class="mr-auto">FireStar</span>
      </b-list-group-item>
    </b-list-group>
                    </div>
                    <div class="col-md-9">

            <b-modal id="bv-modal-example" hide-footer>
                <template v-slot:modal-title>
                <h4>{{edit_add}} Employee</h4>
                </template>
                <div class="d-block">
                

                <div class="container">
                <div class="row">
                    <div class="col-md-12">
                        <b-alert v-model="showDismissibleAlert" variant="danger" dismissible>
                        {{alertFailedmsg}}
                        </b-alert>
                        <b-alert
                        :show="dismissCountDown"
                        dismissible
                        variant="warning"
                        @dismissed="dismissCountDown=0"
                        @dismiss-count-down="countDownChanged"
                        >
                        {{alertFailedmsg}}
                        </b-alert>
                        <form method="post" @submit.prevent="">
                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="First Name">Full Name</label>
                                    <input type="text" class="form-control" name="name" v-model="employeeForm.name" placeholder="Enter Full Name">
                                    <input type="hidden" class="form-control" name="id" v-model="employeeForm.id">
                                </div>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="Last Name">Position</label>
                                    <select name="position" v-model="employeeForm.position" id="position" class="form-control">
                                        <option disabled value="">Select Position</option>
                                        <option value="Business Analyst">Business Analyst</option>
                                        <option value="Project Manager">Project Manager</option>
                                        <option value="Research Engineer">Research Engineer</option>
                                        <option value="Software Engineer">Software Engineer</option>
                                        <option value="Support Manager">Support Manager</option>
                                    </select>
                                </div>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="Salary">Salary</label>
                                    <input type="number" class="form-control" name="salary" v-model="employeeForm.salary" placeholder="Enter Salary" />
                                </div>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="Last Name">Job Type</label>
                                    <select name="job_type" v-model="employeeForm.job_type" id="job_type" class="form-control">
                                        <option disabled value="">Select Job Type</option>
                                        <option value="Full Time">Full Time</option>
                                        <option value="Part Time">Part Time</option>
                                        <option value="Remote">Remote</option>
                                    </select>
                                </div>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="Status">Status</label>
                                    <input type="text" class="form-control" name="status" v-model="employeeForm.status" placeholder="Enter Status" />
                                </div>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <label for="Duration">Duration</label>
                                    <input type="text" class="form-control" name="duration" v-model="employeeForm.duration" placeholder="Enter Duration" />
                                </div>
                            </div>
                        </div>


                        <div class="form-group">
                            <div class="row">
                                <div class="col-sm-12">
                                    <input type="submit" value="Add" v-if="addShow" class="btn btn-primary btn-block" @click="addEmployee()" />

                                    <input type="submit" value="Edit" v-if="editShow" class="btn btn-dark btn-block" @click="EditEmployee()" />

                                </div>
                            </div>
                        </div>
                        </form>
                        <b-alert variant="success" v-model="successDismissibleAlert" show>{{alertSuccessmsg}}</b-alert>
                    </div>
                </div>
            </div>
                

                </div>
                
            </b-modal>
 
            <div class="container mt-5 mb-5">
                <div class="row"><hr/>
                    <div class="col-md-12">
                        <button class="btn btn-success float-right" id="show-btn" @click="$bvModal.show('bv-modal-example'); displayAdd()">add employee</button>
                    </div>
                    
                </div>
            </div>

            <div class="container">
                <div class="row">
                    <div class="col-md-12">
                        <table class="table table-striped">
                                <thead>
                                    <tr>
                                        <th>EMPLOYEE</th>
                                        <th>SALARY</th>
                                        <th>STATUS</th>
                                        <th><i>MANAGE</i></th>
                                    </tr>
                                </thead>

                                <tbody>
                                    <tr v-for="data in empData" v-bind:key="data">
                                        <td class="w-50">
                                            <ul class="employee_holder">
                                                <li class="float-left mr-3"><b-avatar variant="secondary"></b-avatar></li>
                                                <li class="float-left mr-3"><h6>{{data.Name}}</h6><small>{{data.Position}}</small></li>
                                            </ul>
                                        </td>
                                        <td><h6>{{data.Salary}}</h6><small>{{data.Job_Type}}</small></td>
                                        <td><h6>{{data.Status}}</h6><small>{{data.Duration}}</small></td>
                                        <td><b-icon icon="pencil" @click="getSingleEmployee(data.ID); $bvModal.show('bv-modal-example')"></b-icon> &nbsp;|  &nbsp;<b-icon icon="trash"  @click="deleteEmployee(data.ID)"></b-icon></td>
                                    </tr>
                                </tbody>
                            

                            <tr>

                            </tr>

                        </table>
                    </div>
                </div>
            </div>
                    </div>
                </div>
            </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            employeeForm:{
                name:"",
                position:"",
                salary:"",
                job_type:"",
                status:"",
                duration:"",
                id:""
            },
            showDismissibleAlert: false,
            successDismissibleAlert: false,
            alertFailedmsg: "",
            alertSuccessmsg: "",

            dismissSecs: 5,
            dismissCountDown: 0,
            empData:[],
            empID:"",
            editShow:false,
            addShow:true,
            edit_add:"Add"
        }
    },
    methods:{
        countDownChanged(dismissCountDown) {
        this.dismissCountDown = dismissCountDown
        },
        showAlert() {
            this.dismissCountDown = this.dismissSecs
        },
        addEmployee:function(){
             if(this.employeeForm.name == "" || this.employeeForm.position == "" || this.employeeForm.salary == "" || this.employeeForm.job_type == "" || this.employeeForm.status == "" || this.employeeForm.duration == "")
                {
                    this.showAlert();
                    this.alertFailedmsg = "Please fill all Fields";  
                }
                else
                {
                    this.$http.post("http://localhost:8000/api/employee",{name:this.employeeForm.name,position:this.employeeForm.position,salary:this.employeeForm.salary,job_type:this.employeeForm.job_type,status:this.employeeForm.status,duration:this.employeeForm.duration})
                    .then((data)=>{
                        const message = data.body.message;
                       if(message == "Employee added successfully")
                       {
                            this.successDismissibleAlert = true;
                            this.alertSuccessmsg = message;
                            this.emptyEmpForm();
                            this.getAllEmployee();
                       }

                    })
                    .catch((error)=>{
                        console.log(error);
                    });
                }
        },
        emptyEmpForm()
        {
            this.employeeForm.name = "";
            this.employeeForm.position = "";
            this.employeeForm.salary = "";
            this.employeeForm.status = "";
            this.employeeForm.job_type  = "";
            this.employeeForm.duration = "";
        },
        getAllEmployee:function(){
            this.$http.get("http://localhost:8000/api/employee/api_token=823090f139c9e99414c7826bca6c01e51fd76b9f")
        .then((response)=>{
            this.empData = response.body;
            console.log(response);
            })
            .catch((error)=>{
                console.log(error);
            });
        },

        getSingleEmployee:function(id){
            this.empID = id;
            this.$http.get("http://localhost:8000/api/employee/api_token=823090f139c9e99414c7826bca6c01e51fd76b9f/id="+this.empID)
                    .then((response)=>{
                        this.employeeForm.id = response.body.ID;
                        this.employeeForm.name = response.body.Name;
                        this.employeeForm.position = response.body.Position;
                        this.employeeForm.salary = response.body.Salary;
                        this.employeeForm.job_type = response.body.Job_Type;
                        this.employeeForm.status = response.body.Status;
                        this.employeeForm.duration = response.body.Duration;
        
                        this.editShow=true;
                        this.addShow=false;
                        this.edit_add="Edit";

                    })
                    .catch((error)=>{
                        console.log(error);
                    });
        },
        EditEmployee:function(){
             if(this.employeeForm.name == "" || this.employeeForm.position == "" || this.employeeForm.salary == "" || this.employeeForm.job_type == "" || this.employeeForm.status == "" || this.employeeForm.duration == "")
                {
                    this.showAlert();
                    this.alertFailedmsg = "Please fill all Fields";  
                }
                else
                {
                    this.$http.put("http://localhost:8000/api/employee/api_token=823090f139c9e99414c7826bca6c01e51fd76b9f/id="+this.employeeForm.id,{name:this.employeeForm.name,position:this.employeeForm.position,salary:this.employeeForm.salary,job_type:this.employeeForm.job_type,status:this.employeeForm.status,duration:this.employeeForm.duration,id:this.employeeForm.id})
                    .then((data)=>{
                        const message = data.body.message;
                       if(message == "Employee updated successfully!")
                       {
                            this.successDismissibleAlert = true;
                            this.alertSuccessmsg = message;
                            this.emptyEmpForm();
                            this.employeeForm.id = "";
                            this.getAllEmployee();
                            this.editShow=false;
                            this.addShow=true;
                            this.edit_add="Add";
                            
                       }
                       else
                       {
                            this.showAlert();
                            this.alertFailedmsg = message;  
                       }

                    })
                    .catch((error)=>{
                        console.log(error);
                    });
                }
        },
        deleteEmployee:function(id){
            const employee_id = id;

    if(confirm("Are you sure you want to delete Employee ?"))
        {
            this.$http.delete("http://localhost:8000/api/employee/api_token=823090f139c9e99414c7826bca6c01e51fd76b9f/id="+employee_id,{id:employee_id})
                    .then((data)=>{
                        const message = data.body.message;
                       if(message == "Employee deleted successfully!")
                       {
                            this.successDismissibleAlert = true;
                            this.alertSuccessmsg = message;
                            this.getAllEmployee();
                       }
                       else
                       {
                            this.showAlert();
                            this.alertFailedmsg = message;  
                       }

                    })
                    .catch((error)=>{
                        console.log(error);
                    });
            }
        },

        displayAdd:function(){
                            
                this.editShow=false;
                this.addShow=true;
                this.edit_add="Add";
                this.emptyEmpForm();
        }
    },
    created(){
        this.$http.get("http://localhost:8000/api/employee/api_token=823090f139c9e99414c7826bca6c01e51fd76b9f")
        .then((response)=>{
            this.empData = response.body;
            console.log(response);
            })
            .catch((error)=>{
                console.log(error);
            });
    }
}
</script>

<style scoped>
h3{
    color:white;
    text-align: center;
}
.employee_holder
{
    padding: 0;
    margin: 0;
}
.employee_holder li{
    list-style:none;
}
.employee_holder li h3{
    color:black;
}
.employee_holder li small{
    color:rgb(124, 121, 121);
}
</style>