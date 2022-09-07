<script setup>
import { Head, Link } from "@inertiajs/inertia-vue3";
import { ref, reactive, watch } from "vue";
import ListItem from "@/TodoComponents/ListItem.vue";
import TodoForm from "@/TodoComponents/TodoForm.vue";

defineProps({
  canLogin: Boolean,
  canRegister: Boolean,
  todos:Object
});

const show = ref(false);
const hide=()=>{
    show.value=false
}
</script>

<template>
  <Head title="Welcome" />

  <div class=" relative flex items-top justify-center min-h-screen bg-gray-100 dark:bg-gray-900 sm:items-center sm:pt-0 " >
    <div v-if="canLogin" class="hidden fixed top-0 right-0 px-6 py-4 sm:block">
      <Link v-if="$page.props.auth.user" :href="route('dashboard')" class="text-sm text-gray-700 dark:text-gray-500 underline" >Dashboard</Link>
      <template v-else>
        <Link :href="route('login')" class="text-sm text-gray-700 dark:text-gray-500 underline" >Log in</Link>
        <Link v-if="canRegister" :href="route('register')" class="ml-4 text-sm text-gray-700 dark:text-gray-500 underline" >Register</Link>
      </template>
    </div>
    <div class="w-1/2   max-w-7xl  fixed top-12">
      <h1 class="text-2xl font-bold text-center">待辦事項</h1>
      <button @click="show = true" class="py-1 px-3 bg-sky-300 rounded-xl shadow-lg  text-sky-900 ">新增</button>
        <TodoForm :show="show" @hide="hide"/>
      <div>
        <!-- v-for="todo,idx in todos" :key="idx" ref="items" -->
        <ListItem
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
        />
      </div>
    </div>
  </div>
</template>
