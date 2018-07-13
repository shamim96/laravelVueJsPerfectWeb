<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header"><h2>All To DO List
                    <span class="float-right"><button class="btn btn-sm btn-success" data-toggle="modal" data-target="#addTaskModel">+</button>
                    </span>
                    </h2></div>

                    <div class="card-body">
                       <ul class="list-group">
                           <li class="list-group-item" v-for="t in tasks.data">{{t.id}}: {{t.name}}
                           <span class="float-right"><button class="btn btn-sm btn-primary">Add</button> | <button class="btn btn-sm btn-danger">Delete</button> | <button class="btn btn-sm btn-info">Preview</button></span>
                           </li>

                       </ul>

                        <pagination :data="tasks" @pagination-change-page="getResults"></pagination>
                        <!--<pagination :data="tasks">
                            <span slot="pre-nav">&lt; Previous</span>
                            <span slot="next-nav">Next &gt;</span>
                        </pagination>-->
                    </div>
                </div>
            </div>
        </div>
        <div id="model">
            <addTask></addTask>
        </div>
    </div>
</template>
<script type="text/javascript">
    Vue.component('pagination', require('laravel-vue-pagination'));
    Vue.component('addTask',require('./AddTaskModelComponent'));
    export default {

        data() {
            return {
                // Our data object that holds the Laravel paginator data
                tasks: {},
            }
        },

        mounted() {
            // Fetch initial results
            this.getResults();
        },

        methods: {
            // Our method to GET results from a Laravel endpoint
            getResults(page = 1) {
                axios.get('http://localhost/laravel/vuejs/public/tasks?page=' + page)
                    .then(response => {
                        this.tasks = response.data;
                    });
            }
        }

    }
    /*export default{
        data(){
            return{
              tasks:{},
            }
        },
        methods:{
// Our method to GET results from a Laravel endpoint
            getResults(page = 1) {
                axios.get('http://localhost/laravel/vuejs/public/tasks?page=' + page)
                    .then(response => {
                        this.tasks = response.data;
                    });
            }
        },
        created(){
            axios.get('http://localhost/laravel/vuejs/public/tasks')
                .then((response)=>this.tasks = response.data)
                .catch((error)=>console.log("error"))
            console.log("task component loaded....");
        }
    }*/
</script>
<style type="text/css" scoped>

</style>