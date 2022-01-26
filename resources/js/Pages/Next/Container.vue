<template>
     <app-layout title="Dashboard">
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg container p-5">
                        <h2 class="text-align-center">Add New User</h2>
                         <div class="md:flex md:items-center mb-6">
                            <div class="md:w-1/3">
                            <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
                                Name
                            </label>
                            </div>
                            <div class="md:w-2/3">
                            <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-green-100" id="inline-full-name" v-model="item.name" type="text">
                            </div>
                            <div class="md:w-1/3">
                            <label class="block text-gray-500 font-bold md:text-right mb-1 md:mb-0 pr-4" for="inline-full-name">
                                Phone
                            </label>
                            </div>
                            <div class="md:w-2/3">
                            <input class="bg-gray-200 appearance-none border-2 border-gray-200 rounded w-full py-2 px-4 text-gray-700 leading-tight focus:outline-none focus:bg-white focus:border-green-100" id="inline-full-name" v-model="item.phone" type="text">
                            </div>
                        </div>
                         <button 
                           class="shadow bg-purple-500 hover:bg-purple-400 focus:shadow-outline focus:outline-none text-white font-bold py-2 px-4 rounded"
                         @click="save"
                         >Save</button>
                </div>
                <!-- bootstrap view stystem
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
                </table> -->
                <div class="py-5">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-3">
                <div class="bg-white overflow-hidden shadow-xl bg sm:rounded-lg">
                    <div class="flex flex-col">
                    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                        <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
                            <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50">
                                <tr>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                    Name
                                </th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                    Phone
                                </th>
                                <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">
                                    Status
                                </th>
                                </tr>
                            </thead>
                            <tbody class="bg-white divide-y divide-gray-200">
                                <tr
                                    v-for="item in lists"
                                    :key="item.id">
                                <td class="px-6 py-4 whitespace-nowrap">
                                   {{ item.name }}
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    {{ item.phone }}
                                </td>
                                <td class="px-6 py-4 whitespace-nowrap">
                                    <span style="align-item: right;">
                                        <button class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">View</button>
                                                <button class="bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow" 
                                                @click="deleteTel(item.id)"
                                                >Delete</button>
                                    </span>
                                </td>
                                </tr>

                                <!-- More people... -->
                            </tbody>
                            </table>
                        </div>
                        </div>
                    </div>
                    </div>
                </div>
            </div>
        </div>
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
                    axios.delete('/api/tel/' + id);
                }
                catch(e){
                    console.log(e)
                }
            }
            
        }
    })
</script>
