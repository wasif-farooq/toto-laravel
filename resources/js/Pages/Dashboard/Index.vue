<template>
    <layout>
        <div class="container">
            <div class="row justify-content-center">
                <div class="col-md-6">
                    <div class="card">

                        <div class="card-header text-center">Todo List
                            <inertia-link class="btn btn-primary" href="/create">Add</inertia-link>
                        </div>

                        <div class="card-body">
                            <ul>

                                <li class="d-md-flex justify-content-between" v-for="todo in todos" :key="todo.id">

                                    <div v-if="todo.completed == 1">
                                        <inertia-link :href="$route('toggle',todo)" class="fas fa-check" style="color:green"></inertia-link>
                                    </div>
                                    <div v-else>
                                        <inertia-link :href="$route('toggle',todo)" class="fas fa-check"
                                                      style="color: darkgrey"></inertia-link>
                                    </div>
                                    <div v-if="todo.complete == 1">
                                        <inertia-link :href="$route('show',todo)" style="text-decoration: line-through;">
                                                {{ todo.title }}
                                        </inertia-link>
                                    </div>
                                    <div v-else>
                                        <inertia-link :href="$route('show',todo)"><p>{{ todo.title }}</p></inertia-link>
                                    </div>
                                    <inertia-link :href="$route('show',todo)"><p>{{ getExpireAt(todo.expire_at) }}</p></inertia-link>

                                    <inertia-link :href="$route('delete',todo)" class="fas fa-times"></inertia-link>

                                </li>
                            </ul>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </layout>
</template>

<script>
import Layout from "../../Shared/layout";
import Donebutton from "../../components/donebutton";
import moment from "moment";
import "moment-timezone";


export default {
    props: {
        'todos': Array,
        'complete': String,
    },
    components: {Donebutton, Layout},
    methods: {
        getExpireAt(data) {
            const timezone = moment.tz.guess()
            console.log("timezone :", timezone, data, new Date(data))
            return moment.tz(data, 'utc').tz(timezone).format('YYYY-MM-DD hh:mm:ss A')
        }
    }
}
</script>
<style>

</style>
