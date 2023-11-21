<script lang="ts">
    import { ulid, decodeTime } from "ulid";
    import { onMount } from "svelte";

    let ulidInput = "";

    let generatedULID = "";

    onMount(() => {
        console.log(ulid());
    });

    function detectTimeFromULID(id: string): string {
        try {
            const t = decodeTime(id);
            const d = new Date(t);
            const date = d.toLocaleDateString("ja-JP");
            const time = d.toLocaleTimeString();
            return `${t},  ${date} ${time}`;
        } catch (e) {
            return "failed to decode";
        }
    }

    function generateULID(): string {
        const id = ulid();
        generatedULID = id;
        return id;
    }
</script>

<main>
    <h1>ulid utility</h1>

    <div>
        <h2>show unixtime</h2>
        <p>
            <label for="ulidInput">input ulid</label>
        </p>
        <input type="text" id="ulidInput" bind:value={ulidInput} />

        <p>
            unixtime:
            <code>
                {ulidInput
                    ? detectTimeFromULID(ulidInput)
                    : "Please fill with ulid"}
            </code>
        </p>
    </div>

    <hr />

    <div>
        <h2>generate ulid</h2>

        <button on:click={generateULID}>generate </button>

        <p>
            result:
            <code>{generatedULID}</code>
        </p>

        <p>
            time: <code>{detectTimeFromULID(generatedULID)}</code>
        </p>
    </div>
</main>

<style>
</style>
