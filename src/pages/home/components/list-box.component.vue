<template>
    <section id="watch-list-container">
        <ul>
            <li id="watch-list"
                :class="{'already-watched': movies.alreadyWatched}" 
            >
                {{movies.title}}
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    props:["movies"]
}
</script>

<style>

</style>
