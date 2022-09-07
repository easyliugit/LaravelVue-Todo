<script setup>
import { ref ,reactive } from 'vue';
import { useForm } from '@inertiajs/inertia-vue3'

const props=defineProps({show:Boolean})
const emits=defineEmits(['hide'])
const form = useForm({ 
    todo: "", 
    due: "", 
    type: 1 });

const addTodo = () => {
  form.post(route('add.todo'),{
    onSuccess:()=>{
        form.todo="";
        form.due="";
        form.type=1
    },
    onFinish:()=>{
        emits('hide')
    }
  })
};
</script>
<template>
    <div id="addForm" v-if="show" class="p-4 border-blue-600 border w-full my-6">
        <div class="my-2">
            <label class="inline-block w-16 ">事項:</label>
            <input type="text" v-model="form.todo" />
        </div>
        <div class="my-2">
            <label class="inline-block w-16 ">到期日:</label>
            <input type="date" v-model="form.due" />
        </div>
        <div class="my-2">
            <label class="inline-block w-16 ">重要性:</label> 
            <select name="type" v-model="form.type">
                <option value="1">很重要</option>
                <option value="2">普通</option>
                <option value="3">不重要</option>
            </select>
        </div>
    
        <button @click="addTodo" class="rounded-lg bg-blue-600 text-blue-100 py-1.5 px-4 my-2">新增</button>
    </div>
</template>