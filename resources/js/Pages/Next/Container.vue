<template>
    <app-layout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Next
                
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                        <h2>I'm From form component !</h2>
                        <label stylle="margin-right: 13px;">Name</label>
                        <input 
                            type="text"
                            placeholder="Enter Name"
                            v-model="item.name"
                         />
                         <br style="margin: 20px 0;">
                        <label stylle="margin-right: 10px;">Phone</label>
                        <input 
                            type="text"
                            placeholder="Enter Phone"
                            v-model="item.phone"
                         />
                         <br style="margin: 20px 0;">
                         <button 
                         style="padding: 5px;
                         margin: 5px; border-radius: 4px; background: green; color: #fff;"
                         @click="save"
                         >Save</button>
                </div>
                <div v-if="lists.length > 0">
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

                    })
                }catch(e){
                    console.log(e);
                }
            },
            deleteTel(id){
                try{
                    axios.delete('/api/tel/${id}')
                    .then(res => this.fetchAll());
                }
                catch(e){
                    console.log(e)
                }
            }
        }
    })
</script>
