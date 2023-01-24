<script setup>
defineProps(['inicio', 'fin', 'leg']);



</script>

<template>
    <nav aria-label="Page navigation example">
        <ul class="pagination">
            <li><button class="page-link page-item" @click="$emit('previous')" :disabled="inicio === 0">Previous {{
                inicio
            }}</button></li>
            <li><button class="page-link page-item" @click="$emit('nextpage')" :disabled="fin >= leg">Next {{
                fin
            }}</button></li>

        </ul>
    </nav>
</template>


<style>

</style>