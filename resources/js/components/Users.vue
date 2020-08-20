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
                                <th>Modify</th>
                            </tr>
                            </thead>
                            <tbody>
                            <tr>
                                <td>183</td>
                                <td>John Doe</td>
                                <td>11-7-2014</td>
                                <td><span class="tag tag-success">Approved</span></td>
                                <td>
                                    <a href="#">
                                    <i class="fa fa-edit"></i>
                                    </a>
                                    /
                                    <a href="#">
                                        <i class="fa fa-trash"></i>
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
                                   placeholder="Password"
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
                        <button type="button" class="btn btn-primary">Create</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Users",

        data(){
            return {
                form: new form({
                    name: '',
                    email: '',
                    password:'',
                    type: '',
                    bio:'',
                    photo: ''
                })
            }
        }
    }
</script>

<style scoped>

</style>
