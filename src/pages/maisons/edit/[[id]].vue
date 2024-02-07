<script setup lang="ts">
import { ref } from "@vue/reactivity" ;
import AfficheMaison from "@/components/AfficheMaison.vue" ;
import { useRoute } from 'vue-router/auto'
const route = useRoute('/maisons/edit/[[id]]')
const maison = ref({})
async function upsertMaison(dataForm, node) {
    const { data, error } = await supabase.from("Maisons").upsert(dataForm);
    if (error) node.setErrors([error.message])
    else {
        node.setErrors([]);
        router.push({ name: "/maisons/edit/[[id]]", params: { id: data[0].id } });
    }

}


</script>
<template>
    <div>
        <div class="p-2">
        <h2 class="text-2xl">Résultat (Prévisualisation)</h2>
        <AfficheMaison v-bind="maison"/>
        </div>
        <div class="p—2">
        <FormKit @submit="upsertMaison" type="form" v-model="maison" :config="{
            classes: {
                input: 'p-1 rounded border-gray-300 shadow-sm border',
                label: 'text-gray-600 mb-12',
            },
        }">
        <div class="flex gap-5 p-2 my-12">
            
            <FormKit name="nomMaison" placeholder="nom"  />
            <FormKit name="surface" placeholder="Surface" />
            <FormKit name="prix" placeholder="prix" type="number" />
            <FormKit name="nbrSDB" placeholder="Salle de bain" type="number" />
            <FormKit name="nbrChambres" placeholder="Chambres" type="number" />
        </div>
        <FormKit name="favori" label="mettre en valeur" type="checkbox"/>


        </FormKit>
        </div>
    </div>

</template >