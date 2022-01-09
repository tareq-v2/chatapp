<template>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <!-- <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script> -->
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Next
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg container p-5">
                        <h2 class="text-align-center">Add New User</h2>
                        <label stylle="margin-right: 13px;">Name</label>
                        <input 
                            type="text"
                            placeholder="Enter Name"
                            v-model="item.name"
                            class="form-control"

                         />
                         <br style="margin: 20px 0;">
                        <label stylle="margin-right: 10px;">Phone</label>
                        <input 
                            type="text"
                            placeholder="Enter Phone"
                            v-model="item.phone"
                            class="form-control"
                         />
                         <br style="margin: 20px 0;">
                         <button 
                          class="btn btn-primary"
                         @click="save"
                         >Save</button>
                </div>
                <table class="table" v-if="lists.length > 0">
                    <thead>
                        <tr>
                            <h6 class="text-align-center">All Users</h6>
                        </tr>
                    </thead>
                    <tbody>
                        <tr 
                        v-for="item in lists"
                        :key="item.id"
                        >
                        <div class="row justify-content-center">
                            <div class="col-6">
                                {{ item.name }}  and {{ item.phone }}
                            </div>
                            <div class="col-6">
                                <span style="align-item: right;">
                                    <button style="padding: 5px;
                            margin: 5px; border-radius: 4px; background: green; color: #fff;">View</button>
                                    <button 
                                    @click="deleteTel(item.id)"
                                    style="padding: 5px;
                            margin: 5px; border-radius: 4px; background: red; color: #fff;">Delete</button>
                                </span>
                            </div>
                        </div>
                        </tr>
                        
                    </tbody>
                </table>
                <!-- <div v-if="lists.length > 0">
                    <ul>
                        <li
                            v-for="item in lists"
                            :key="item.id"
                        >
                            {{ item.name }}  and {{ item.phone }}
                            <span style="align-item: right;">
                                <button style="padding: 5px;
                         margin: 5px; border-radius: 4px; background: green; color: #fff;">View</button>
                                <button 
                                @click="deleteTel(item.id)"
                                style="padding: 5px;
                         margin: 5px; border-radius: 4px; background: red; color: #fff;">Delete</button>
                            </span>
                        </li>
                    </ul>
                </div> -->
            </div>
            
        </div>
    </app-layout>
</template>
<style>
    ul{
        display: flex;
        justify-content: space-around;
    }
</style>
<script>
    import { defineComponent } from 'vue'
    import AppLayout from '@/Layouts/AppLayout.vue'
    import Welcome from '@/Jetstream/Welcome.vue'

    export default defineComponent({
        components: {
            AppLayout,
            Welcome,
        },
        data(){
            return {
                lists: [],
                item: {
                    name: '',
                    phone: ''
                }
            }
        },
        mounted(){
            this.fetchAll();
        },
        methods: {
            fetchAll(){
                axios.get('/api/tel')
                .then(res => this.lists = res.data)
            },
            save(){
                try{
                    axios.post('/api/tel', this.item)
                    .then(res => {
                        console.log(res);
                    })
                }catch(e){
                    console.log(e);
                }
            },
            deleteTel(id){
                try{
                    axios.delete('/api/tel/$id')
                    .then(res => {
                        console.log(res);
                        this.fetchAll(id);
                    });
                }
                catch(e){
                    console.log(e)
                }
            }
        }
    })
</script>
