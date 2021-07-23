<template>
    <div>
        <button class="btn btn-info float-right" @click="onNew">
            New Profile
        </button>
        <h5>Vet View</h5>
        <hr>
        <form action="" @submit.prevent="onSave">
            <b-form-group label="Name">
                <b-form-input v-model="vet.name"></b-form-input>
                </b-form-group>
    
                <b-form-group label="Pet Name">
                <b-form-input v-model="vet.pet"></b-form-input>
                </b-form-group>
    
                <b-form-group label="Pet Gender">
                <b-form-input v-model="vet.gender"></b-form-input>
                </b-form-group>
    
                <b-form-group label="Breed">
                <b-form-input v-model="vet.breed"></b-form-input>
                </b-form-group>
    
                <b-form-group label="Vaccine Name">
                <b-form-input v-model="vet.vaccine"></b-form-input>
                </b-form-group>
    
                <b-form-group label="Date Vaccinated">
                <b-form-input type="date" v-model="vet.date"></b-form-input>
                </b-form-group>
    
            <b-form-group>
               <button class="btn btn-primary" type="submit">Save Changes</button>
                <button class="btn btn-danger" type="button" @click="onDelete" v-if="vet.id">Delete</button>
            </b-form-group>
        </form>
    </div>
</template>
<script>
export default {
    props: {
        vet: {}
    },
    methods: {
        async onSave() {
            try {
                if(!this.vet.id) {
                    await this.$axios.post('/api/vets', this.vet)
                }else {
                    await this.$axios.put('/api/vets/'+this.vet.id, this.vet)
                }
                this.$emit('saved');
            }catch(err) {
                alert(err.response.data.message)
            }
        },
        onNew() {
            this.$emit('newItem')
        },
        async onDelete() {
            try {
                this.$axios.delete('/api/vets/'+this.vet.id)
                this.$emit('deleted')
            }catch(err) {
                alert(err.response.data.message)
            }
        }
    }
}
</script>

