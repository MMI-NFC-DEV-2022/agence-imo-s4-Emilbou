<script setup lang="ts">
import { ref } from "@vue/reactivity";
import { useRoute, useRouter } from 'vue-router/auto'
import { supabase } from '@/supabase'
const route = useRoute('/quartier/edit/[id]')
const router = useRouter()
const quartier = ref({})


// @ts-ignore
async function upsertquartier(dataForm, node) {
    const { data, error } = await supabase.from("quartier").upsert(dataForm).select('id');
    if (error) node.setErrors([error.message])
    else {
        console.log("data id :", data[0].id);

        node.setErrors([]);
        router.push("/quartier/");
    }

}

if (route.params.id) {
    // On charge les données de la maison
    let { data, error } = await supabase
        .from("quartier")
        .select("*")
        .eq("id", route.params.id);
    if (error) console.log("n'a pas pu charger le table quartier :", error);
    else quartier.value = (data as any[])[0];
}


</script>
<template>
    <div>
        <div class="p-2">
            <h2 class="text-2xl">Résultat (Prévisualisation)</h2>

            <p>{{ quartier.nom_quartier }}</p>
        </div>
        <div class="p—2">
            <FormKit @submit="upsertquartier" type="form" v-model="quartier" :config="{
                classes: {
                    input: 'p-1 rounded border-gray-300 shadow-sm border',
                    label: 'text-gray-600 mb-12',
                },
            }">
                <div class="flex gap-5 p-2 my-12">

                    <FormKit name="nom_quartier" placeholder="nom" />

                </div>


            </FormKit>
        </div>
    </div>
</template >