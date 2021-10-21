<template>
    <q-page>
        <div class="row">
            <q-table
                title="Nginx Table"
                :rows="nginxs"    
                :columns="columns"
                row-key="name"
                class="col"
                :filter="filter">
            
            <template v-slot:top-right>
            <q-input borderless dense debounce="300" v-model="filter" placeholder="Search">
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
      </template>

            </q-table>
        </div>

    </q-page>
</template>

<script>
import { ref } from 'vue'
export default {
    name: 'PageNginx',
    data () {
        return {
            columns: [
                { name: 'ip_address', label: 'Ip Address', field: 'ip_address', align: 'center', sortable: true },
                { name: 'date', label: 'Date', field: 'date', align: 'center', sortable: true },
                { name: 'method', label: 'Method', field: 'method', align: 'left', sortable: true },
                { name: 'status_server', label: 'Status Server', field: 'status_server', align: 'center', sortable: true },
                { name: 'ping_ms', label: 'Ping Ms', field: 'ping_ms', align: 'center', sortable: true },
                { name: 'site_request', label: 'Site Request', field: 'site_request', align: 'left', sortable: true },
                { name: 'rt', label: 'rt', field: 'rt', align: 'center', sortable: true },
                { name: 'uct', label: 'uct', field: 'uct', align: 'center', sortable: true },
                { name: 'uht', label: 'uht', field: 'uht', align: 'center', sortable: true },
                { name: 'urt', label: 'urt', field: 'urt', align: 'center', sortable: true },
                { name: 'gz', label: 'gz', field: 'gz', align: 'center', sortable: true }
            ],
            nginxs: [],
            filter: ref('')
        }
    },
    mounted () {
        this.getNginxs()
    },
    methods: {
        getNginxs () {
          this.$axios.get('http://192.168.4.74:2000/nginx.php')
            .then((res) => {
              this.nginxs = res.data
              console.log(res.data)
            })
            .catch((err) => {
                console.log(err)
            })
        }
    }
}
</script>
