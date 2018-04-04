<template>
    <tr>
        <td>{{ customer.name }}</td>
        <td>{{ customer.email }}</td>    //I don't know why it says "unresolved parameter email
    </tr>
</template>

<script>
    export default {
        props:['customer']
    }
</script>