<template>
    <div>
        <sui-card>
            <sui-card-content>
                <sui-card-header> {{ author }}</sui-card-header>
                <!-- <sui-card-meta>2 days ago</sui-card-meta> -->
                <sui-card-description>
                <p>
                    <em>{{ mood }}</em>
                </p>
                </sui-card-description>
            </sui-card-content>
        </sui-card>
    </div>
</template>
<script>
export default {
    name: 'Mood',
    props: {
        author: {
            type: String,
            required: true
        },
        mood: {
            type: String,
            required: true
        }
    }
};
</script>
