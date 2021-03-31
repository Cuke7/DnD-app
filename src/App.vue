<template>
    <v-app>
        <v-app-bar app color="primary" dark>
            <v-app-bar-title>
                Générateur de rencontre DnD
            </v-app-bar-title>
        </v-app-bar>

        <v-main>
            <RencontreUI @newMonsters="newMonsters"></RencontreUI>
            <draggable class="list-group"  v-bind="dragOptions" @start="drag = true" @end="drag = false">
                <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                    <Monster v-for="monster in monsters" v-bind:key="monster.key" :monster="monster"></Monster>
                    <Player v-for="player in players" v-bind:key="player.key" :player="player"></Player>
                </transition-group>
            </draggable>
        </v-main>
    </v-app>
</template>

<script>
import Monster from "./components/Monster";
import RencontreUI from "./components/RencontreUI";
import draggable from "vuedraggable";
import Player from "./components/Player";

export default {
    name: "App",

    components: {
        Monster,
        draggable,
        RencontreUI,
        Player,
    },

    data: () => ({
        monsters: [],
        drag: false,
        players: [
            {
                nom: "Caedus",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/_resampled/ResizedImageWzQ4Niw2NzZd/eldritch.jpg",
                CA: 17,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                key: 997,
            },
            {
                nom: "Corinne",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/paladin.jpg",
                CA: 16,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                key: 998,
            },
            {
                nom: "Stor",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/druide.jpg",
                CA: 15,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                key: 999,
            },
            {
                nom: "Matt",
                avatar_url: "https://www.aidedd.org/assets/regles/classes/sorcier.jpg",
                CA: -1,
                caracs: { FOR: "20 (+5)", DEX: "14 (+2)", CON: "10 (+0)", INT: "10 (+0)", SAG: "11 (+0)", CHA: "13 (+1)" },
                key: 1000,
            },
        ],
    }),
    methods: {
        newMonsters: function(monsters) {
            this.monsters = monsters;
        },
    },
    // For the drag stuff
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
};
</script>

<style scoped>
.button {
    margin-top: 35px;
}
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
