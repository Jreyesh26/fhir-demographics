<script lang="ts">
  import { onMount } from "svelte";
  import { fhir } from "./fhir";
  import { navigate } from "svelte-routing";

  let loading: boolean = false;
  export let id;
  let form;
  console.log(id);
  async function handleSubmit(e: any) {
    loading = true;
    if (id) {
      const r = await fhir.put(`/Patient/${id}`, { ...e.detail, id });
    } else {
      const r = await fhir.post("/Patient", e.detail);
    }

    loading = false;
    navigate("/", { replace: true });
  }
  onMount(async () => {
    if (id) {
      const r = await fhir.get(`/Patient/${id}`);
      const resource = r.data;
      form.import(resource);
    }
  });
</script>

<h1>Patient Registration</h1>
<mb-fhir-form
  bind:this={form}
  class="flex flex-col gap-3"
  on:mb-submit={handleSubmit}
>
  <mb-context path="resourceType" bind="Patient"></mb-context>
  <mb-input path="name[0].given" label="Nombre del paciente" />
  <mb-date label="Fecha de nacimiento" path="birthDate" />
  <mb-buttons datatype="code" label="Genero" path="gender">
    <mb-option value="male" label="Masculino" />
    <mb-option value="female" label="Femenino" />
    <mb-option value="other" label="Otro" />
  </mb-buttons>
  <mb-submit>
    <sl-button {loading} class="info">Enviar</sl-button>
  </mb-submit>
</mb-fhir-form>
