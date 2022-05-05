<template>
        <div id="viz"></div>
</template>

<script>
import NeoVis from 'neovis.js';
export default {
  name: 'GraphCanvas',
  props: {
  }, 
  data() {
      return{Viz: {}
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
            initial_cypher: "MATCH (n)-[p]-(m) optional match (o) RETURN *"
        };

        this.Viz = new NeoVis(config);
        this.Viz.render();
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
