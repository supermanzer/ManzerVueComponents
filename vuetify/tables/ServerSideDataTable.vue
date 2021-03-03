<!-- 
    components/General/Tables/ssDataTable.vue

    Defines a Vuetify data table configured for server side sorting, pagination, and searching
-->
<template>
  <div class="wrapper">
      <v-data-table
      :items="records"
      :headers="headers"
      hide-default-footer
      class="elevation-1"
      :options.sync="options"
      :items-per-page="records.length"
      :page.sync="options.page"
      :no-data-text="noDataText"
      >
        <template v-slot:top>
            <slot name="table-top"></slot>
        </template>
        <template v-slot:item.actions="{ item }">
            <slot name="table-actions" v-bind:item="item">
                <!-- Use this slot in parent pages to trigger specific record action -->
            </slot>
        </template>
      </v-data-table>
      <v-pagination :length="pageCount" v-model="options.page" :total-visible="11"></v-pagination>
  </div>
</template>

<script>
export default {
    name: 'ServerSideDataTable',
    props: {
        headers: {type: Array, required: true},
        records: {type: Array, required: true},
        pageCount: {type: Number, required: true},
        noDataText: {type: String, required: false, default: 'No Data'},
    },
    data() {
        return {
            options: {
                page: 1
            }
        }
    },
    watch: {
        options: {
            handler() {
                this.$emit('table-change', this.options)
            },
            deep: true
        },
    }
}
</script>

<style>

</style>