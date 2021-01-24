<template>
    <div class="px-4 py-5 ">
        <title>
            Time converter
        </title>
        <section>
            <div class="sm:px-10">

                <div class="p-6  border-b border-gray-200">
                    <div class="mt-8 text-2xl">
                        Convertisseur de secondes en jours, heures, minutes
                    </div>
                    <div class="mt-6 text-gray-500">
                        Que représentent la différence entre un million et un milliard, à part 3 zéros supplémentaires ?
                        Il est difficile de se représenter la signification d'une valeur, sans un repère familier dans lequel l'inscrire.
                        Et si on convertit cette valeur pour la faire apparaitre dans un autre plan référentielle, est ce que ça devient plus claire ?
                    </div>
                </div>

                <form class="flex py-6 space-x-4">
                    <div class="flex-none items-center justify-center py-6 px-6">
                        <seconds-input id="seconds" v-model="seconds" placeholder="Nombre de secondes"/>
                    </div>

                    <div class="flex-grow items-center justify-center py-6 px-6">
                        <div class="font-semibold text-sm text-gray-600 py-6" >
                            <template v-if="seconds == 1 || !seconds">
                                <span> Est équivalent à </span>
                            </template><template v-else>
                                <span> Sont équivalentes à </span>
                            </template>
                            <span class="" v-if="seconds">{{ echoAll }}</span>
                        </div>
                    </div>
                </form>

            </div>
        </section>
    </div>
</template>

<script>

    import SecondsInput from '@/TimeConverter/SecondsInput';

    export default {
        name: "Converter",
        components: {
            SecondsInput
        },
        data() {
            return {
                seconds: 0,
            }
        },
        computed: {
            echoAll: function() {
                return  this.secondsToDhms();
            },
            echoDay: function() {
                return  this.secondsToDhms('day');
            },
            echoHour: function() {
                return  this.secondsToDhms('day');
            },
            echoMinute: function() {
                return  this.secondsToDhms('day');
            },
            echoSeconde: function() {
                return  this.secondsToDhms('day');
            },
            secondsFormated: function (){
                if(!this.seconds){
                    return;
                }
                return new Intl.NumberFormat('fr-FR', { style: 'decimal'}).format(this.seconds);
            }
        },
        methods: {
            secondsToDhms: function (toReturn) {
                let seconds = Number(this.seconds);
                var d = Math.floor(seconds / (3600*24));
                var h = Math.floor(seconds % (3600*24) / 3600);
                var m = Math.floor(seconds % 3600 / 60);
                var s = Math.floor(seconds % 60);

                // const toReturn = $return || 'all';
                var dDisplay = d > 0 ? d + (d == 1 ? " jour, " : " jours, ") : "";
                var hDisplay = h > 0 ? h + (h == 1 ? " heure, " : " heures, ") : "";
                var mDisplay = m > 0 ? m + (m == 1 ? " minute, " : " minutes, ") : "";
                var sDisplay = s > 0 ? s + (s == 1 ? " seconde" : " secondes") : "";

                switch(toReturn){
                    case "day":
                        return d;
                        break;
                    case "hour":
                        return h;
                        break;
                    case "minute":
                        return m;
                        break;
                    case "second":
                        return s;
                        break;
                    default:
                        return dDisplay + hDisplay + mDisplay + sDisplay;
                }
            },
        }
    }
</script>


<style scoped lang="scss">
    @import "../../sass/app.scss";
    .flex-auto {
        border: 0px solid black;
    }

</style>


