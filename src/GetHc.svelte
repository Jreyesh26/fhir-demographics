<!-- HC.svelte -->
<script lang="ts">
    import { onMount } from "svelte";
    import { fhir } from "./fhir";
    import { Link } from "svelte-routing";

    let patient = {};
    let observations = [];
    let encounters = [];

    export let id;

    onMount(async () => {
        try {
            // Obtener información del paciente
            const patientResponse = await fhir.get(`/Patient/${id}`);
            patient = patientResponse.data;

            // Obtener observaciones asociadas al paciente
            const observationResponse = await fhir.get(
                `/Observation?subject=Patient/${id}`,
            );
            observations =
                observationResponse.data?.entry?.map(
                    (entry) => entry.resource,
                ) || [];

            // Obtener encuentros asociados al paciente
            const encounterResponse = await fhir.get(
                `/Encounter?subject=Patient/${id}`,
            );
            encounters =
                encounterResponse.data?.entry?.map((entry) => entry.resource) ||
                [];
        } catch (error) {
            console.error(
                "Error al obtener datos del paciente, sus observaciones o encuentros:",
                error,
            );
        }
    });
</script>

<Link to="/">
    <sl-button type="primary">Volver a la lista de pacientes</sl-button>
</Link>

<h1 class="text-2xl">
    Historia Clínica de {patient.name?.[0]?.given?.join(" ")}
</h1>

<div>
    <h2 class="text-xl">Datos del paciente:</h2>
    <p><strong>Nombre:</strong> {patient.name?.[0]?.given?.join(" ")}</p>
    <p><strong>Fecha de nacimiento:</strong> {patient.birthDate}</p>
    <p><strong>Género:</strong> {patient.gender}</p>
</div>

<div>
    <h2 class="text-xl">Observaciones:</h2>
    <ul>
        {#each observations as observation}
            <li>
                {observation.code?.coding?.[0]?.display}: {observation
                    .valueQuantity?.value}
                {observation.valueQuantity?.unit}
            </li>
        {/each}
    </ul>
</div>

<div>
    <h2 class="text-xl">Encuentros:</h2>
    <ul>
        {#each encounters as encounter}
            <h2 class="text-xl">Información del Encuentro:</h2>
            <p><strong>ID del Encuentro:</strong> {encounter.id}</p>
            <p>
                <strong>Fecha de última actualización:</strong>
                {encounter.meta?.lastUpdated}
            </p>
            <p>
                <strong>Participante:</strong>
                {encounter.participant?.[0]?.type?.[0]?.coding?.[0]?.display}
            </p>
        {/each}
    </ul>
</div>
