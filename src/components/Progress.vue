<script setup>
defineProps({
    value: Number,
    max: Number
})

</script>

<template>
    <div>
        Etape {{ value + 1 }}/{{ max }}
        <progress :value="value" :max="max"/>
    </div>
</template>