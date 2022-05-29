<template>
        <div id="viz"></div>
        <AddNpc :viz="Viz"/>
        <DeleteNpc :viz="Viz"/>
        <AddRelation :viz="Viz" @connect="prepareConnection"/>
</template>

<script>
//import NeoVis from 'neovis.js'
import NeoVis from '../neovis/neovis';
import AddNpc from './AddNpc.vue';
import DeleteNpc from './DeleteNpc.vue';
import AddRelation from './AddRelation.vue';
export default {
  name: 'GraphCanvas',
    components: {
    AddNpc,
    DeleteNpc,
    AddRelation
},
  props: {
  }, 
  data() {
      return {
          Viz: {},
          id0: -1,
          realation: ""
      } 
  },
  methods: {
      prepareConnection(value) {
        this.id0 = value.id0,
        this.realation = value.relation
      }
  },
  mounted: function(){
        var config = {
            container_id: "viz",
            server_url: "neo4j://b700f583.databases.neo4j.io",
            server_user: "neo4j",
            server_password: "ik92Fa_WUGsyM5t49MoAuSFz0JershP-9qNTw2TP2ig",
            labels: {
                "NPC": {
                    "caption": "name",
                }
            },
            relationships: {
                "fucks": {
                    "caption": true
                }
            },
            initial_cypher: "MATCH (n)-[p]-(m) optional match (o) RETURN *" //TODO Error without any relation
        };

        this.Viz = new NeoVis(config);
        this.Viz.render();

        this.Viz.registerOnEvent('clickNode', async (properties) => {
        const nodeId = properties.nodeId;
        if(this.id0 != -1){
            //TOODO

                    const neo4j = require('neo4j-driver')
                    const uri = "neo4j://b700f583.databases.neo4j.io"
                    const user =  "neo4j"
                    const password = "ik92Fa_WUGsyM5t49MoAuSFz0JershP-9qNTw2TP2ig"

                    const driver = neo4j.driver(uri, neo4j.auth.basic(user, password))
                    const session = driver.session()

                    try {
                    const result = await session.run(
                        'MATCH (a:NPC), (b:NPC) WHERE id(a) = $id0 AND id(b) = $id1 CREATE (a)-[r:'+this.realation+']->(b) RETURN type(r)',
                        {
                            id0: this.id0,
                            id1 : nodeId
                        }
                    )

                    const singleRecord = result.records[0]
                    const node = singleRecord.get(0)
                    console.log(node)

                    } finally {
                    await session.close()
                    }
                    await driver.close()
                    this.Viz.reload()





            console.log("connnect")
            this.id0 = -1;
        }
    // Do something
        });
        console.log(this.Viz);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
html, body {
    font: 16pt arial;
}

#viz {
    width: 900px;
    height: 700px;
    border: 1px solid lightgray;
    font: 22pt arial;
}
</style>
