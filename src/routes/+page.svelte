<script lang="ts">
  import { Input } from "$lib/components/input";
  import { Button } from "$lib/components/button";
</script>

<Input name="prenom" label="Prénom" placeholder="Your name" fill={true} />

<Button name="btn">
  <span>Submit</span>
</Button>