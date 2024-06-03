<!-- getHC.svelte -->
<script lang="ts">
  import { onMount } from "svelte";
  import { fhir } from "./fhir";
  import { Link } from "svelte-routing";

  let patients = [];

  onMount(async () => {
    const response = await fhir.get("/Patient");
    patients = response.data?.entry?.map((entry) => entry.resource) || [];
  });
</script>

<Link to="patient">
  <sl-button type="primary">Nuevo paciente</sl-button>
</Link>
<Link to="load">
  <sl-button type="primary">Cargar pacientes predefinidos</sl-button>
</Link>

<h1 class="text-2xl">Registro de pacientes</h1>

<div>
  <table>
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Fecha de Nacimiento</th>
        <th>Género</th>
        <th>Ver Historia Clínica</th>
      </tr>
    </thead>
    <tbody>
      {#each patients as patient}
        <tr>
          <td
            ><Link to={`patient/${patient.id}`}
              >{patient.name[0]?.given?.join(" ")}</Link
            ></td
          >
          <td>{patient.birthDate}</td>
          <td>{patient.gender}</td>
          <td><Link to={`hc/${patient.id}`}>Ver HC</Link></td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>
