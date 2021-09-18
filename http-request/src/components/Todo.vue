<template>
     <div class="row">
          <div
            class="col-md-6 offset-md-3 border d-flex flex-row justify-content-between align-items-center p-2"
          >
            <span>{{ todo.text }}</span>
            <!-- <span>{{ todo.id }}</span> -->
            <button class="btn btn-danger" @click="$emit('deleteTodo', todo.id)">Delete</button>
          </div>
     </div>
</template>

<script>
export default ({
    props : ["todo"]
})
</script>
