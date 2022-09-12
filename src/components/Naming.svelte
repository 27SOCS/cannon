<script>
  const computerTypes = [
    { id: "W", type: "Workstation" },
    { id: "L", type: "Laptop" },
    { id: "T", type: "Tablet" },
  ];
  const squadrons = [
    { id: "SOG", name: "27 SOG" },
    { id: "3OS", name: "3 SOS" },
    { id: "9OS", name: "9 SOS" },
    { id: "12OS", name: "12 SOS" },
    { id: "16OS", name: "16 SOS" },
    { id: "17OS", name: "17 SOS" },
    { id: "20OS", name: "20 SOS" },
    { id: "33OS", name: "33 SOS" },
    { id: "56IS", name: "56 SOIS" },
    { id: "310OS", name: "310 SOS" },
    { id: "318OS", name: "318 SOS" },
    { id: "OSS", name: "27 SOSS" },
    { id: "AMXS", name: "27 SOAMXS" },
    { id: "9AMU", name: "9 AMU" },
    { id: "16AMU", name: "16 AMU" },
    { id: "727MX", name: "727 SOAMXS" },
    { id: "3AMU", name: "3 AMU" },
    { id: "20AMU", name: "20 AMU" },
    { id: "MXG", name: "27 SOMXG" },
    { id: "MUNS", name: "27 SOMS" },
    { id: "SOW", name: "27 SOW" },
    { id: "AOS", name: "27 SOAOS" },
    { id: "CPTS", name: "27 SOCPTS" },
    { id: "MSG", name: "27 SOMSG" },
    { id: "CES", name: "27 SOCES" },
    { id: "CS", name: "27 SOCS" },
    { id: "LRS", name: "27 SOLRS" },
    { id: "CONS", name: "27 SOCONS" },
    { id: "SFS", name: "27 SOSFS" },
    { id: "FSS", name: "27 SOFSS" },
    { id: "STS", name: "26 STS" },
    { id: "43IS", name: "43 IS" },
    { id: "TRS", name: "373 TRS" },
  ];

  let manufacturer = "other";
  let selectedType;
  let selectedSQ;
  let serial = "";
  $: name = `CZQZ${selectedType || ""}-${selectedSQ}`;

  // Dell uses start
  $: start = serial.substring(0, Math.min(serial.length, 15 - name.length));

  // Default end of serial
  $: end = serial.substring(serial.length - (15 - name.length), serial.length);

  // Surface Pro cuts off first three
  $: surface = serial.substring(3, Math.min(serial.length, 18 - name.length));

  $: finalName = `${name}${manufacturer === "dell" ? start : manufacturer === "surface" ? surface : end}`;
</script>

<div class="mt-6 card w-96 bg-base-200 shadow-xl mx-auto">
  <div class="card-body">
    <div class="form-control w-full max-w-xs">
      <label class="label" for="computer">
        <div
          class="tooltip tooltip-primary tooltip-right"
          data-tip="What type of computer it is"
        >
          <span class="label-text font-bold">Computer type</span>
        </div>
      </label>

      <select bind:value="{selectedType}" class="select select-bordered">
        {#each computerTypes as type}
        <option value="{type.id}">{type.type}</option>
        {/each}
      </select>
    </div>

    <div class="form-control w-full max-w-xs">
      <label class="label" for="squadron"
        ><div
          class="tooltip tooltip-primary tooltip-right"
          data-tip="Which Squadron the computer is going to"
        >
          <span class="label-text font-bold">Squadron</span>
        </div>
      </label>

      <select bind:value="{selectedSQ}" class="select select-bordered">
        {#each squadrons as sq}
        <option value="{sq.id}">{sq.name}</option>
        {/each}
      </select>
    </div>

    <div class="form-control w-full max-w-xs">
      <label class="label" for="serial">
        <div
          class="tooltip tooltip-primary tooltip-right"
          data-tip="Full serial number of computer"
        >
          <span class="label-text font-bold">Serial</span>
        </div>
      </label>
      <input
        bind:value="{serial}"
        type="text"
        placeholder="Type here"
        class="input input-bordered w-full max-w-xs"
      />
    </div>

    <div class="form-control mt-6">
      <span class="label-text font-bold">Manufacturer/Model</span>
      <label class="label cursor-pointer">
        <div class="tooltip tooltip-primary tooltip-right" data-tip="Dell">
          <span class="label-text mt">Dell</span>
        </div>
        <input
          type="radio"
          name="radio-6"
          class="radio"
          bind:group="{manufacturer}"
          value="dell"
          checked
        />
      </label>
    </div>
    <div class="form-control">
      <label class="label cursor-pointer">
        <div class="tooltip tooltip-primary tooltip-right" data-tip="Surface Pro">
          <span class="label-text">Microsoft Surface Pro</span>
        </div>
        <input
          type="radio"
          name="radio-6"
          class="radio"
          bind:group="{manufacturer}"
          value="surface"
        />
      </label>
    </div>
    <div class="form-control">
      <label class="label cursor-pointer">
        <div class="tooltip tooltip-primary tooltip-right" data-tip="Other">
          <span class="label-text">Other</span>
        </div>
        <input
          type="radio"
          name="radio-6"
          class="radio"
          bind:group="{manufacturer}"
          value="other"
        />
      </label>
    </div>
  </div>
</div>

<div class="mx-auto w-96">
  <div class="mt-10">
    <div class="bg-base-200 rounded-2xl shadow-xl p-5">
      <div class="">Name:</div>
      <div class="text-2xl font-bold mx-auto">{finalName.toUpperCase()}</div>
    </div>
  </div>
</div>
