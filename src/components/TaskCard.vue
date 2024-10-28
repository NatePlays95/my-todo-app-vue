<script>
import './TaskCard.css'

export default {
    props: {
        task: String,
        index: Number
    },

    methods: {
        handleDelete() {
            this.$emit("delete-task", this.index);
        }
    }
};

</script>

<template>
    <div className="task-card">
        {{ task }}

        <button 
        className="task-card-delete-btn"
        @click="handleDelete"
        >Delete</button>
    </div>
</template>