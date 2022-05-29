<template>
    <button @click="selectOnClick">
        Add Relationship
    </button>
</template>

<script>
export default {
    name: 'AddRelation',
    props: ["viz"],

    data() {
         return{
            id0: -1,
            relation: "loves"
        }
    },
    methods: {
        async selectOnClick(){
                this.id0 = this.viz.selectedItem
                 this.$emit('connect', {
                    id0: this.id0,
                    relation: this.relation
                })
        },


    } 
}
</script>
