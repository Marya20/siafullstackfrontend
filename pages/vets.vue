<template>
    <div>
        <NavBar />
        <div class="container">
        <div class="row">
            <div class="col-6">
                <h5>List of Vet Profile</h5>
                <ul class="list-group">
                    <li class="list-group-item list-group-item-action" v-for="vet in vets" :key="vet.id" @click="onSelected(vet)">
                        {{vet.name}} <span class="float-right">{{vet.pet}}</span>
                    </li>
                    
                </ul>
            </div>
            <div class="col-4">
                <VetView :vet="selectedVet" @saved="onChanges" @newItem="onNew" @deleted="onChanges"/>
            </div>
        </div>
    </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            vets: [],
            selectedVet: {}
        }
    },
    methods: {
        async getMyVets() {
            await this.$axios.get('/api/vets')
            .then((res)=>{
                if(res.status==200) {
                    this.vets = res.data
                }
            })
        },
        onChanges() {
            this.getMyVets()
            this.selectedVet = {}
        },
        onSelected(vet) {
            this.selectedVet = vet
        },
        onNew() {
            this.selectedVet = {}
        }
    },
    created() {
        this.getMyVets()
    }
}
</script>
<style scoped>
.container{
    margin-top: 50px;
}

</style>
