<template>
    <div class="seconds-input py-2">
        <label class="block">
            <span
                class="info text-sm text-gray-600 px-3 py-2 whitespace-nowrap"
                v-if="value">
                    {{ valueFormatted }}
                    <template v-if="value <= 1">
                        seconde
                    </template><template v-else>
                        secondes
                    </template>
            </span>
            <input class="mt-1 block w-full rounded-md bg-gray-100 border-transparent focus:border-gray-500 focus:bg-white focus:ring-0"
                   type="number"
                   v-model="value"
                   :placeholder="placeholder"/>

        </label>
    </div>
</template>

<script>
    export default {
        name: "SecondsInput",
        props: ["valueProp", "placeholder"],
        data: function() {
            return {
                value: '',
            }
        },
        mounted: function(){
            this.value =  this.valueProp;
        },
        computed: {
            valueFormatted:{
                get: function() {
                    let value = this.value;
                    this.$emit('input', parseInt(value, 10))
                    return (isNaN(value) || '' == value)
                        ? ''
                        : Intl.NumberFormat('fr-FR', { style: 'decimal'}).format(value);
                }
            },
        }
    }
</script>

<style scoped lang="scss">
    .seconds-input {
         position: relative;
        .info {
            position: absolute;
            top: -1.5rem;
            left: 0;
        }
    }
</style>