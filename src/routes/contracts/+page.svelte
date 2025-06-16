<script lang="ts">
  import { SpaceTradersSdk } from "@wwaaijer/space-traders-sdk";
  import { onMount } from "svelte";
  /////

  const api = new SpaceTradersSdk({
    token:
      "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGlmaWVyIjoiQ1lQSE9OIiwidmVyc2lvbiI6InYyLjMuMCIsInJlc2V0X2RhdGUiOiIyMDI1LTA2LTA4IiwiaWF0IjoxNzQ5NDA4ODg3LCJzdWIiOiJhZ2VudC10b2tlbiJ9.Oca_sr5UCZsD7O60O9WeQPmkLYe5FMpwLILKEiDq1BAv22ZW_1aOg1WppS6Lt0iegfbTGBXhnj4NEI_E6mjxUJaGjaeHeNJBBHKtJ83KR1vvsurKMLUXtIHAp1bv33CzADzNQ2Mo1yA_xls83kz58CyFjMF45YXEUS_pWFlzuldSOXpRuyc90u6QnGStdCAtBtI4_YLbyvaF5DP74uTO1-iGlgKdMAySMrFs47nscAXNi2FtcMlKh_WhQGse9s1DiENJZssKJ8F3eo1Sr_ObYbKAwLjr2JEJ75zliVlf7JP8kpHYdS8W-9pVKsCsPTyWepR_G4rJszWq1dQzvWcmsa8naoge9o5r6Y7zXKGQnm91EvBCgn5FJ1GRbaVeGf7XwmgFkLsJTpl5VEsKEK8lLVw1nWatyYYRWydGiCBQGyefarTC8qTCkJ8Rg_v2Cs81EHLfUVD9HlBcH_NBElFPTNgA4dZN-BKQVSkNJ59z7IfbW6toT3H3enMd_F6_KEQr6d9gFaiKYPZSDvy1ufEsZ-OJxNo1SVS78DWtC5yDt3BVOU5Wi8_IegnqtZbMPA3J8A-9hidHbtSq8RbzVtoxwnxt_C6mrM5MQP0xBIMu2GGI3_WweTq-qoYeSWzQpQd0Wb6yWEgMph0KIPTw1ac0fANxfXFcjXViA1BbEKK7fr4",
  })

let available = {}

async function get_available() {
    // await api.acceptContract("cmbrdxmwf95pwuo6xzbm2rg4r");
    available = await api.getContracts()
    console.log(available)
}

  </script>

  <div class="container mx-auto p-4 bg-slate-900">
  <h1>Contracts</h1>

  <p>
    <button
      class="rounded-sm bg-sky-700 hover:bg-sky-600 px-2"
      onclick={() => get_available()}
    >
      Get Available
    </button>
  </p>

  <pre>{available}</pre>
</div>