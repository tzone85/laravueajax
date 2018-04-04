<template>

    <div>

        <form v-on:submit.prevent = "createCustomer" action="post">
            <div class="form-grpup">
                <label>Name</label>

                <input type="text" v-model="customer.name" class="form-control">
            </div>

            <div class="form-grpup">
                <label>Email</label>

                <input type="text" v-model="customer.email" class="form-control">
            </div>

            <div class="form-grpup">

                <input type="submit" class="btn btn-primary" value="Create New Customer">
            </div>

        </form>

        <table class="table table-bordered table-striped table-condensed">
            <thead>
            <tr>
                <th>Name</th>
                <th>Email</th>
            </tr>
            </thead>

            <tbody>
            <customer v-for="customer in customers" :key="customer.id">
            <!--<customer v-for="customer in customers" v-bind:customer="customer">-->

            </customer>
            </tbody>
        </table>
    </div>

</template>

<script>

    import customer from './Customer.vue';
    export default {
        data(){
            return {
                customers: [],
                customer:{
                    name:'',
                    email:''
                }
            }
        },

        component:{ customer },

        create (){
            this.fetchCustomer();
        },

        methods:{
            fetchCustomer(){
                this.$http.get("customer").then(response => { this.customers = response.data.customers});

//                axios.get("customer").then(response => { this.customers = response.data.customers});  // was trying to resolve the problem
            }
        },
        createCustomer(){
            this.$http.post("/customer/", this.customer).then(response => {
               this.customer = response.data.customer;
               console.log(response.data);
            });
        }
    }
</script>
