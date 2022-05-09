<template>
    <button @click="deleteNpc">
        Delete
    </button>
</template>

<script>
export default {
    name: "DeleteNpc",
    props:["viz"],
    methods: {
        async deleteNpc(){
const neo4j = require('neo4j-driver')
            const uri = "neo4j://b700f583.databases.neo4j.io"
            const user =  "neo4j"
            const password = "ik92Fa_WUGsyM5t49MoAuSFz0JershP-9qNTw2TP2ig"

            const driver = neo4j.driver(uri, neo4j.auth.basic(user, password))
            const session = driver.session()

            try {
            const result = await session.run(
                'match (n) where id(n)  = $id detach delete n return n',
                {id: this.viz.selectedItem }
            )

            const singleRecord = result.records[0]
            const node = singleRecord.get(0)

            console.log(node.properties.name)
            } finally {
            await session.close()
            }

            // on application exit:
            await driver.close()
            this.viz.reload()
        }
    }

}
</script>