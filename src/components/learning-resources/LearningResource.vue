<template>
    <li>
        <div>
            <h3>{{title}}</h3>
            <button>Delete</button>
        </div>
        <p>{{description}}</p>
        <nav>
            <a :href="link">View Resource</a>
        </nav>
    </li>
</template>

<script>
export default {
    props: ['title', 'description', 'link']
}
</script>