<script>
  export let medication = {
    name: "", // name of med
    doseOnHand: 0, // dose in mg
    volume: 0, // volume in mL
    adminReason: "", // reason why you are administering
    dose: "", // dose ordered
    route: "" // route to give med
  }
</script>

<main>
  <div class="medication">
    <h2>{medication.name}</h2>
    <p>
      {medication.doseOnHand}mg <br />
      {medication.volume}mL
    </p>
  </div>
</main>

<style>
  div.medication {
    max-width: 300px;
    border: 2px solid rgb(149,117,205);
    background-color: rgba(149, 117, 205, 0.3);
    border-radius: 8px;
    margin: 0 15px;
    padding: 15px;
    flex: 1;
    transition: 150ms;
  }

  div.medication:hover {
    background-color: rgba(149, 117, 205, 0.4);
  }

  div.medication h2 {
    margin: 0;
    line-height: 1;
  }
  div.medication p {
    margin-bottom: 0;
  }
</style>