<script lang="ts">
  import { Router, Link, Route } from "svelte-routing";
  import "medblocks-ui";
  import "medblocks-ui/dist/shoelace";
  import "medblocks-ui/dist/styles.js";
  import "./tailwind.css";
  import PatientRegistration from "./PatientRegistration.svelte";
  import Layout from "./Layout.svelte";
  import List from "./List.svelte";
  import GetHc from "./GetHc.svelte";
  import LoadInformation from "./LoadInformation.svelte";
</script>

<Router>
  <Layout>
    <Route path="/" component={List} />
    <Route path="/patient" component={PatientRegistration} />
    <Route path="/patient/:id" component={PatientRegistration} />
    <Route path="/load" component={LoadInformation} />
    <Route path="/hc/:id" component={GetHc} />
  </Layout>
</Router>
