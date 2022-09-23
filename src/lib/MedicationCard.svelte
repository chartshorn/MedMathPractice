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
    border: 3px solid #65499c;
    background-color: #9575cd;
    border-radius: 8px;
    margin: 0 15px;
    padding: 15px;
    flex: 1;
  }

  div.medication h2 {
    margin: 0;
    line-height: 1;
  }
  div.medication p {
    margin-bottom: 0;
  }
</style>