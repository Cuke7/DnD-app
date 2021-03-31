<template>
    <v-app>
        <v-app-bar app color="primary" dark>
            <v-app-bar-title>
                Générateur de rencontre DnD
            </v-app-bar-title>
        </v-app-bar>

        <v-main>
            <RencontreUI @newMonsters="newMonsters"></RencontreUI>
            <draggable v-if="monsters.length > 0" class="list-group" v-model="monsters" v-bind="dragOptions" @start="drag = true" @end="drag = false">
                <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                    <Monster v-for="monster in monsters" v-bind:key="monster.key" :monster="monster"></Monster>
                </transition-group>
            </draggable>
            <div class="text-center" v-else>
                Aucun monstre trouvé.
            </div>
        </v-main>
    </v-app>
</template>

<script>
import Monster from "./components/Monster";
import RencontreUI from "./components/RencontreUI";
import draggable from "vuedraggable";

export default {
    name: "App",

    components: {
        Monster,
        draggable,
        RencontreUI,
    },

    data: () => ({
        monsters: [],
        drag: false,
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
