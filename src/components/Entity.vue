<template>
    <v-card class="my-6 mx-auto" max-width="1300" dense>
        <v-row align="center" justify="space-around">
            <!--AVATAR-->
            <v-col cols="1" class="text-center">
                <v-avatar size="75">
                    <img alt="Avatar" :src="entity.avatar_url" v-if="entity.isPlayer" />
                    <img alt="Avatar" :src="entity.img_url" v-else-if="entity.img_url" />
                </v-avatar>
            </v-col>

            <!--NAME et FP-->
            <v-col cols="2" class="text-center">
                <strong>{{ entity.nom }}</strong>
                <span v-if="!entity.isPlayer"> ({{ entity.FP }})</span>
            </v-col>

            <!--ATTRIBUTS-->
            <v-col cols="3" class="text-center">
                <v-chip-group column>
                    <v-chip color="red lighten-4" class="ml-0 mr-2 black--text" label small>{{ entity.type }}</v-chip>
                    <v-chip color="blue lighten-4" class="ml-0 mr-2 black--text" label small>{{ entity.alignement }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ entity.vitesse_details }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ entity.taille }}</v-chip>
                </v-chip-group>
            </v-col>

            <!--CA-->
            <v-col cols="1" class="text-center">
                <v-row align="center">
                    <v-icon color="blue">mdi-shield</v-icon>
                    <strong color="blue">{{ entity.CA }}</strong>
                </v-row>
            </v-col>

            <!--PV-->
            <v-col cols="2" class="text-center" v-if="!entity.isPlayer">
                <v-row align="center">
                    <v-icon color="red">mdi-heart</v-icon>
                    <strong>{{ entity.pv_details }}</strong>
                </v-row>
            </v-col>

            <!--INITIATIVE-->
            <v-col cols="1" class="text-center" v-if="entity.isPlayer">
                <v-text-field hide-details color="green" label="Init" prepend-inner-icon="mdi-fast-forward" v-model="entity.init"></v-text-field>
            </v-col>
            <v-col cols="1" class="text-center" v-else>
                <v-row align="center">
                    <v-icon color="green">mdi-fast-forward</v-icon>
                    <strong>15</strong>
                </v-row>
            </v-col>

            <!--DETAILS BOUTON-->
            <v-col v-if="!entity.isPlayer">
                <v-btn icon @click="show = !show">
                    <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
                </v-btn>
            </v-col>
        </v-row>

        <!--DETAILS-->
        <v-expand-transition>
            <div v-show="show">
                <v-divider></v-divider>
                <v-card-text>
                    I'm a thing. But, like most politicians, he promised more than he could deliver. You won't have time for sleeping, soldier, not with all the bed making you'll be doing. Then we'll
                    go with that data file! Hey, you add a one and two zeros to that or we walk! You're going to do his laundry? I've got to find a way to escape.
                </v-card-text>
            </div>
        </v-expand-transition>
    </v-card>
</template>
<script>
export default {
    name: "Entity",
    props: ["entity"],
    data: () => ({
        show: false,
    }),
};
</script>
