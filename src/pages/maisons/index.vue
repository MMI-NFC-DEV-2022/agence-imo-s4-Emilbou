<script setup lang="ts">

import AfficheMaison from '@/components/AfficheMaison.vue';
import {supabase} from '@/supabase'
import type { SchemaOffreMaison } from '@/types';

console.log("supabase :", supabase); // pour vérifier et "garder" supabase dans le code

const { data: Maisons, error } = await supabase
    .from('Maisons')
    .select('*')
console.log(Maisons)


</script>


<template>
    <h1>Bonjour</h1>
    <AfficheMaison v-for="mesMaisons in Maisons" v-bind="mesMaisons"></AfficheMaison>
</template>