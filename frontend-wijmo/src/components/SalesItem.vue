<template>

    <div>
        <div class="detail-title">
        SalesItem
        </div>
        <v-col>
            <div class="label-title">ProductId</div>
            <String label="입력하세요." v-model="value.productId" :editMode="editMode"/>
            <div class="label-title">Quantity</div>
            <Number label="입력하세요." v-model="value.quantity" :editMode="editMode"/>
            <div class="label-title">Price</div>
            <Number label="입력하세요." v-model="value.price" :editMode="editMode"/>
        </v-col>

        <v-card-actions v-if="inList">
            <slot name="actions"></slot>
        </v-card-actions>
    </div>
</template>

<script>
import BaseEntity from './base-ui/BaseEntity'

export default {
    name: 'SalesItem',
    mixins:[BaseEntity],
    components:{
    },
    data: () => ({
        path: 'salesItems'
    }),
    watch: {
        value(val) {
            this.$emit('input', val);
        }
    },
    async created(){
        if (this.value && this.value.id !== undefined) {
            this.value = await this.repository.findById(this.value.id)
        }
    },
    methods: {
        pick(val){
            this.$emit('input', val);
        },
    }
}
</script>

