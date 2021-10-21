<template>
    <q-page>
        <div class="row">
            <q-table
                title="Uwsgi Table"
                :rows="uwsgis"    
                :columns="columns"
                row-key="name"
                class="col"
            />
        </div>

    </q-page>
</template>

<script>
export default {
    name: 'PageUwsgi',
    data () {
        return {
            columns: [
                { name: 'address_space_usage', label: 'Address Space Usage', field: 'address_space_usage', align: 'center', sortable: true },
                { name: 'rss_usage', label: 'Rss Usage', field: 'rss_usage', align: 'center', sortable: true },
                { name: 'pid', label: 'Pid', field: 'pid', align: 'center', sortable: true }
            ],
            uwsgis: []
        }
    },
    mounted () {
        this.getUwsgis()
    },
    methods: {
        getUwsgis () {
          this.$axios.get('http://192.168.4.74:2000/uwsgi.php')
            .then((res) => {
              this.uwsgis = res.data
              console.log(res.data)
            })
            .catch((err) => {
                console.log(err)
            })
        }
    }
}
</script>
