<script setup lang="ts">
import { supabase } from "../../supabase";
import groupBy from "lodash/groupBy";
const { data, error } = await supabase.from("quartier_commune").select("*");
if (error) console.log("n'a pas pu charger la table quartiercommune :", error);
</script>

<template>
  <section class="flex flex-col">
    <h3 class="text-2xl">Liste des quartiers</h3>
    <ul>
      <li v-for="(lesquartiers, nomCommune) in (Object.groupBy(data, v => v.nomCommune))">
<h2>{{ nomCommune }}</h2>
<li v-for="quartierObject in lesquartiers">
    <div>{{ quartierObject.nom_quartier }}</div>
</li>
      </li>
    </ul>
  </section>
  <Disclosure
        v-for="(listeQuartier, libelleCommune) in groupBy(
            data,
            'nomCommune'
        )"
        :key="libelleCommune"
      />
</template>