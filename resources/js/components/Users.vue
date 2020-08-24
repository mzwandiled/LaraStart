<template>
    <div class="container">
        <div class="row mt-5">
            <div class="col-md-12">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">Users Table</h3>

                        <div class="card-tools">
                          <button class="btn btn-success" data-toggle="modal" data-target="#addNew">Add New <i class="fa fa-user-plus fa fw"></i></button>
                        </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body table-responsive p-0">
                        <table class="table table-hover text-nowrap">
                            <thead>
                            <tr>
                                <th>ID</th>
                                <th>Name</th>
                                <th>Email</th>
                                <th>Type</th>
                                <th>Registered At</th>
                                <th>Modify</th>
                            </tr>
                            </thead>
                            <tbody>
                            <tr v-for="user in users" :key="user.id">
                                <td>{{user.id}}</td>
                                <td>{{user.name}}</td>
                                <td>{{user.email}}</td>
                                <td>{{user.type | textUppercase}}</td>
                                <td>{{user.created_at| myDate}}</td>
                                <td>
                                    <a href="#" >
                                    <i class="fa fa-edit"></i>
                                    </a>
                                    /
                                    <a href="#" @click="deleteUser(user.id)">
                                        <i class="fa fa-trash text-red"></i>
                                    </a>

                                </td>
                            </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- /.card-body -->
                </div>
                <!-- /.card -->
            </div>
        </div>
        <!-- Modal -->
        <div class="modal fade" id="addNew" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="addNewn">Add New</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <form @submit.prevent="createUser" >
                    <div class="modal-body">
                        <div class="form-group">
                            <input v-model="form.name" type="text" name="name"
                                   placeholder="Name"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('name') }">
                            <has-error :form="form" field="name"></has-error>
                        </div>
                        <div class="form-group">

                            <input v-model="form.email" type="text" name="email"
                                   placeholder="Email"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('email') }">
                            <has-error :form="form" field="email"></has-error>
                        </div>
                        <div class="form-group">
                            <input v-model="form.password" type="password" name="password"
                                   placeholder="Password" autocomplete="on"
                                   class="form-control" :class="{ 'is-invalid': form.errors.has('password') }">
                            <has-error :form="form" field="password"></has-error>
                        </div>
                        <div class="form-group">
                            <textarea name="bio" id="bio" cols="60" rows="3" class="" v-model="form.bio" placeholder="Shot bio user info">
                            </textarea>
                        </div>
                        <div class="form-group">
                            <select name="type" id="type" class="form-control" v-model="form.type">
                                <option value="">Select user Role</option>
                                <option value="admin">Admin</option>
                                <option value="standard">Standard</option>
                                <option value="author">Author</option>
                            </select>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-danger" data-dismiss="modal">Close</button>
                        <button type="submit" class="btn btn-primary">Create</button>
                    </div>
                    </form>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Users",

        data:function(){
            return {
                form: new form({
                    name: '',
                    email: '',
                    password:'',
                    type: '',
                    bio:'',
                    photo: ''
                }),
                users:[]
            }
        },
        methods: {
            deleteUser(id){
                swal.fire({
                    title: 'Are you sure?',
                    text: "You won't be able to revert this!",
                    icon: 'warning',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Yes, delete it!'
                }).then((result) => {

                    //send a request to the server
                    this.form.delete().then(()=>{
                        swal.fire(
                            'Deleted!',
                            'Your file has been deleted.',
                            'success'
                        )

                    }).catch(()=>{
                        swal.fire(
                            'Failed!',
                            'There was something wrong',
                            'warning'
                        )
                    })

                })
            },
            loadUsers(){
              axios.get('api/users').then(({data})=>(this.users = data.data));
            },
            createUser(){
                this.$Progress.start();
                //submit the post via the POst
                this.form.post('/api/users')
                    .then(()=>{
                        Fire.$emit('AfterCreate');
                        $('#addNew').modal('hide');
                        toast.fire({
                            icon: 'success',
                            title: 'User Created successfully'
                        })
                        this.$Progress.finish();

                    }).catch(()=>{
                        //console.log(errors)
                });

            }
        },
        filters: {
            capitalize:function(value){
                    if(!value)
                        return ''
                value = value.toString()
                return value.charAt(0).toUpperCase()+ value.slice(1)
            }
        },
        created() {
            this.loadUsers()
            //setInterval(()=>this.loadUsers(),3000)
            Fire.$on('AfterCreate',()=>{
                this.loadUsers();
            });
        }
    }
</script>

<style scoped>

</style>
