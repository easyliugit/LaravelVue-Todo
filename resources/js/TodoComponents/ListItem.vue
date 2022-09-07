<script setup>
    import { propsToAttrMap } from '@vue/shared';
    import {ref,reactive,watch} from 'vue'
    import { useForm } from '@inertiajs/inertia-vue3'
import { parserOptions } from '@vue/compiler-dom';

    const props=defineProps({todo:Object})
    const emits=defineEmits(['delTodo'])
    const item=ref();
    const edit=ref(false)

    const form = useForm({ 
    id:props.todo.id,
    todo: props.todo.todo, 
    due: props.todo.due, 
    type: props.todo.type });

    const delTodo=()=>{
        form.delete(route('destroy.todo',form.id))
    }

    const editTodo=()=>{
      edit.value=true
    }

    const updateTodo=()=>{
        form.put(route('update.todo',form.id),{
            onSuccess:()=>{
                edit.value=false;
            }
        })
    }
    </script>
    <template>
    
    <div class="w-full flex justify-between m-2 border border-slate-700 py-2 px-4" ref="item">
        <div class="w-4/12">
            <span v-if="!edit">{{ todo.todo }}</span>
            <input v-if="edit" type="text" v-model="form.todo">
        </div>
        <div class="w-1/4">
            <span  v-if="!edit">{{ todo.due }}</span>
            <input v-if="edit" type="date" v-model="form.due">
        </div>
        <div class="w-1/6">
            <span  v-if="!edit">{{ todo.type }}</span>
    
            <select v-if="edit" name="type"  v-model="form.type">
                <option value="1">很重要</option>
                <option value="2">普通</option>
                <option value="3">不重要</option>
            </select>
        </div>
        <div class="w-1/4">{{ todo.status }}</div>
        <button class="w-1/12"  v-if="edit" @click="updateTodo">OK</button>
        <button class="w-1/12"  v-if="!edit" @click="editTodo">編輯</button>
        <button class="w-1/12"  v-if="!edit" @click="delTodo">X</button>
      </div>
    
    </template>
