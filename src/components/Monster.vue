<template>
    <v-card class="my-6 mx-12">
        <v-row align="center" justify="space-around">
            <v-col cols="2" class="text-center" v-if="monster.img_url">
                <v-avatar size="150">
                    <img v-if="monster.img_url" alt="Avatar" :src="monster.img_url" />
                    <v-icon v-else>mdi-play</v-icon>
                </v-avatar>
            </v-col>

            <v-col cols="5" class="text-center">
                <v-row>
                    <strong>{{ monster.nom }}</strong>
                    <span class="grey--text">({{ monster.FP }}) </span>
                </v-row>
                <v-row>
                    <v-simple-table dense>
                        <thead>
                            <tr>
                                <th>FOR</th>
                                <th>DEX</th>
                                <th>CON</th>
                                <th>INT</th>
                                <th>SAG</th>
                                <th>CHA</th>
                            </tr>
                        </thead>
                        <tbody>
                            <td v-for="(value, index) in monster.caracs" v-bind:key="index">
                                <v-chip color="grey" class="ma-2 black--text" label small>{{ value }}</v-chip>
                            </td>
                        </tbody>
                    </v-simple-table>
                </v-row>
            </v-col>

            <v-col cols="2">
                <v-chip-group column>
                    <v-chip color="red lighten-4" class="ml-0 mr-2 black--text" label small>{{ monster.type }}</v-chip>
                    <v-chip color="blue lighten-4" class="ml-0 mr-2 black--text" label small>{{ monster.alignement }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ monster.vitesse_details }}</v-chip>
                    <v-chip color="green lighten-4" class="ml-0 mr-2 black--text" label small>{{ monster.taille }}</v-chip>
                </v-chip-group>
            </v-col>

            <v-col cols="2">
                <v-row>
                    <v-text-field class="ma-2" hide-details color="red" label="PV" prepend-inner-icon="mdi-heart" v-model="monster.PV"></v-text-field>
                </v-row>
                <v-row>
                    <v-text-field class="ma-2" hide-details color="blue" label="CA" prepend-inner-icon="mdi-shield" v-model="monster.CA"></v-text-field>
                </v-row>
                <v-row>
                    <v-text-field class="ma-2" hide-details color="green" label="Init" prepend-inner-icon="mdi-fast-forward" v-model="monster.init"></v-text-field>
                </v-row>
            </v-col>

            <v-col cols="1">
                <v-btn icon @click="show = !show">
                    <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
                </v-btn>
            </v-col>
        </v-row>

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
    name: "Monster",
    props: ["monster"],
    data: () => ({
        show: false,
    }),
};
</script>
