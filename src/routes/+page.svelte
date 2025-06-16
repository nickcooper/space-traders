<script lang="ts">
  import { SpaceTradersSdk } from "@wwaaijer/space-traders-sdk";
  import P5 from "p5-svelte";
  import { onMount } from "svelte";
  /////

  const api = new SpaceTradersSdk({
    token:
      "eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZGVudGlmaWVyIjoiQ1lQSE9OIiwidmVyc2lvbiI6InYyLjMuMCIsInJlc2V0X2RhdGUiOiIyMDI1LTA2LTA4IiwiaWF0IjoxNzQ5NDA4ODg3LCJzdWIiOiJhZ2VudC10b2tlbiJ9.Oca_sr5UCZsD7O60O9WeQPmkLYe5FMpwLILKEiDq1BAv22ZW_1aOg1WppS6Lt0iegfbTGBXhnj4NEI_E6mjxUJaGjaeHeNJBBHKtJ83KR1vvsurKMLUXtIHAp1bv33CzADzNQ2Mo1yA_xls83kz58CyFjMF45YXEUS_pWFlzuldSOXpRuyc90u6QnGStdCAtBtI4_YLbyvaF5DP74uTO1-iGlgKdMAySMrFs47nscAXNi2FtcMlKh_WhQGse9s1DiENJZssKJ8F3eo1Sr_ObYbKAwLjr2JEJ75zliVlf7JP8kpHYdS8W-9pVKsCsPTyWepR_G4rJszWq1dQzvWcmsa8naoge9o5r6Y7zXKGQnm91EvBCgn5FJ1GRbaVeGf7XwmgFkLsJTpl5VEsKEK8lLVw1nWatyYYRWydGiCBQGyefarTC8qTCkJ8Rg_v2Cs81EHLfUVD9HlBcH_NBElFPTNgA4dZN-BKQVSkNJ59z7IfbW6toT3H3enMd_F6_KEQr6d9gFaiKYPZSDvy1ufEsZ-OJxNo1SVS78DWtC5yDt3BVOU5Wi8_IegnqtZbMPA3J8A-9hidHbtSq8RbzVtoxwnxt_C6mrM5MQP0xBIMu2GGI3_WweTq-qoYeSWzQpQd0Wb6yWEgMph0KIPTw1ac0fANxfXFcjXViA1BbEKK7fr4",
  });

  /////
  let data = $state({});

  $effect(() => {
    const savedData = localStorage.getItem("space_traders");
    if (savedData) data = JSON.parse(savedData);
  });

  $effect(() => {
    localStorage.setItem("space_traders", JSON.stringify(data));
  });
  /////

  async function get_waypoints() {
    let waypoints = [];
    const res = await api.getSystemWaypoints("X1-VP71", {
      page: 1,
      limit: 20,
    });
    waypoints.push(...res.data);
    for (let page = 2; page <= Math.ceil(res.meta.total / 20); page++) {
      const res = await api.getSystemWaypoints("X1-VP71", {
        page: page,
        limit: 20,
      });
      waypoints.push(...res.data);
    }
    data.waypoints = waypoints;
  }

  async function g() {
    // let maxX = 0;
    // let minX = 0;
    // let maxY = 0;
    // let minY = 0;
    // data.waypoints.forEach((i) => {
    //     if (i.x > maxX) maxX = i.x;
    //     if (i.x < minX) minX = i.x;
    //     if (i.y > maxY) maxY = i.y;
    //     if (i.y < minY) minY = i.y;
    // });
  }
  
  let points = [];

  onMount(() => {
    
points = data.waypoints.map((w, i) => {
      if (w.symbol == "X1-VP71-A1") console.log("found");
      if (w.x == 26 && w.y == -2) console.log("found", w.symbol);
      return {
        x: w.x * 0.5,
        y: w.y * 0.5,
        c: w.symbol == "X1-VP71-A1" ? "#f00" : "#0f0",
      };
    });
    
  });

    

  let width = 55;
    let height = 55;

    const sketch = (p5) => {
      p5.setup = () => {
        p5.createCanvas(1200, 1200);
      };

      p5.draw = () => {
        // p5.circle(p5.width / 2, p5.height / 2, 20);
        points.forEach((item) => {
          p5.fill(item.c);
          p5.circle(item.x + 600, item.y + 600, 12);
        });
      };
    };

  /////
</script>

<div class="container mx-auto p-4 bg-slate-900">
  <h1>System</h1>

  <p>
    <button
      class="rounded-sm bg-sky-700 hover:bg-sky-600 px-2"
      onclick={() => get_waypoints()}
    >
      Test
    </button>
  </p>

  <P5 {sketch} />
</div>
