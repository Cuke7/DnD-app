<template>
    <v-app>
        <v-app-bar app color="primary" dark>
            <v-app-bar-title>
                Générateur de rencontre DnD
            </v-app-bar-title>
        </v-app-bar>

        <v-main>
            <RencontreUI @newMonsters="newMonsters"></RencontreUI>
            <draggable class="list-group" v-model="entities" v-bind="dragOptions" @start="drag = true" @end="drag = false">
                <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                    <Entity v-for="(entity, index) in entities" v-bind:key="index" :entity="entity"></Entity>
                </transition-group>
            </draggable>
        </v-main>
    </v-app>
</template>

<script>
//import Monster from "./components/Monster";
import RencontreUI from "./components/RencontreUI";
import draggable from "vuedraggable";
//import Player from "./components/Player";
import Entity from "./components/Entity";

export default {
    name: "App",

    components: {
        //Monster,
        draggable,
        RencontreUI,
        //Player,
        Entity,
    },

    data: () => ({
        monsters: [],
        drag: false,
        entities: [],
        entities_default: [
            {
                nom: "Caedus",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/_resampled/ResizedImageWzQ4Niw2NzZd/eldritch.jpg",
                CA: 17,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                type: "Haut-elfe",
                taille: "M",
                alignement: "CB",
                vitesse_details: "9 m",
                isPlayer: true,
            },
            {
                nom: "Corinne",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/paladin.jpg",
                CA: 16,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                type: "Dragon",
                taille: "M",
                alignement: "NN",
                vitesse_details: "8 m",
                isPlayer: true,
            },
            {
                nom: "Stor",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/druide.jpg",
                CA: 15,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                type: "Humain",
                taille: "M",
                alignement: "CN",
                vitesse_details: "9 m",
                isPlayer: true,
            },
            {
                nom: "Matt",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/sorcier.jpg",
                CA: -1,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                type: "Haut-elfe",
                taille: "TP",
                alignement: "CM",
                vitesse_details: "5 m",
                isPlayer: true,
            },
        ],
    }),
    methods: {
        newMonsters: function(monsters) {
            this.entities = this.entities_default;
            this.entities = this.entities.concat(monsters);
        },
    },
    // For the dragagable stuff
    computed: {
        dragOptions() {
            return {
                animation: 200,
                group: "description",
                disabled: false,
                ghostClass: "ghost",
            };
        },
    },
    mounted: function() {
        this.$nextTick(function() {
            this.entities = this.entities_default;
        });
    },
};
</script>


<style scoped>
/* CSS styles for the transitionof the draggable components */
.flip-list-move {
    transition: transform 0.5s;
}
.no-move {
    transition: transform 0s;
}
.ghost {
    opacity: 0;
    background: #c8ebfb;
}
</style>
