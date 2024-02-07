<script lang="ts">
    import * as Select from "$lib/components/ui/select";
    import * as Card from "$lib/components/ui/card";
    import { page } from '$app/stores';
    import "../../app.pcss";
    let times: string[] = [];
    const xtimes = [
        "1/1/2024 @ 10.00",
        "1/1/2024 @ 11.00",
        "1/1/2024 @ 12.00",
        "1/1/2024 @ 13.00",
        "1/1/2024 @ 14.00",
        "1/1/2024 @ 15.00",
        "1/1/2024 @ 16.00",
        "1/1/2024 @ 17.00",
        "1/1/2024 @ 18.00",
        "1/1/2024 @ 19.00",
        "1/1/2024 @ 20.00",
    ];
    const ytimes = [
        "1/2/2024 @ 10.00",
        "1/2/2024 @ 11.00",
        "1/2/2024 @ 12.00",
        "1/2/2024 @ 13.00",
        "1/2/2024 @ 14.00",
        "1/2/2024 @ 15.00",
        "1/2/2024 @ 16.00",
        "1/2/2024 @ 17.00",
        "1/2/2024 @ 18.00",
        "1/2/2024 @ 19.00",
        "1/2/2024 @ 20.00",
    ];
    const ztimes = [
        "1/3/2024 @ 10.00",
        "1/3/2024 @ 11.00",
        "1/3/2024 @ 12.00",
        "1/3/2024 @ 13.00",
        "1/3/2024 @ 14.00",
        "1/3/2024 @ 15.00",
        "1/3/2024 @ 16.00",
        "1/3/2024 @ 17.00",
        "1/3/2024 @ 18.00",
        "1/3/2024 @ 19.00",
        "1/3/2024 @ 20.00",
    ];
    const dft = "No time slot chosen";
    const dfp = "No 'book' chosen"
    let sTime = dft;
    let sProf = dfp;
    let cProf: string;
    /**
     * function to submit booking request
    */
    function sbmt() {
        if(sTime !== dft) {
            alert("booked!");
        }
    }
    /**
     * function to move time slot to booking card
     * @param t
     */
    function chs(t: string) {
        sTime = t;
        sProf = cProf;
    }
    /**
     * function to save current selected book
    */
    function slct(p: string | undefined) {
        if(p !== undefined) {
            cProf = p.trim();
            if(cProf === "Professor X") {
                times = xtimes;
            } else if(cProf === "Professor Y") {
                times = ytimes;
            } else if(cProf === "Professor Z") {
                times = ztimes;
            } else {
                console.log('ERR: type not valid', sProf);
            }
        }
    }
</script>

<main class="flex p-10 gap-6 bg-gray-400">
    <div class="p-4 rounded-md border w-1/2 items-center self-center">
        <div class="p-10">
            <Select.Root onSelectedChange={val => slct(val?.label)}>
                <Select.Trigger class="w-[180px]">
                    <Select.Value placeholder="Choose somebody!" />
                </Select.Trigger>
                <Select.Content>
                    <Select.Item value="light">Professor X</Select.Item>
                    <Select.Item value="dark">Professor Y</Select.Item>
                    <Select.Item value="system">Professor Z</Select.Item>
                </Select.Content>
            </Select.Root>
        </div>
        <div class="p-10">
            <Card.Root>
                <Card.Header>
                    <Card.Title>{sTime}</Card.Title>
                    <Card.Description>{sProf}</Card.Description>
                </Card.Header>
                <Card.Content>
                    <button class="bg-gray-300 rounded-md p-2"
                            on:click={() => {sbmt()}}>Book Now!</button>
                </Card.Content>
                <Card.Footer>
                    <p>
                        Read more about {sProf}
                        <a href="/ourbooks" aria-current={$page.url.pathname === '/ourbooks'}>
                            here
                        </a>
                    </p>
                </Card.Footer>
            </Card.Root>
        </div>
    </div>
    <div class="bg-red-300 h-96 w-1/2 rounded-md border overflow-y-scroll items-center self-center">
        {#each times as time}
            <div class="bg-white p-2 border text-center">
                {time}
                <button class="bg-gray-300 rounded-md text-center px-2" 
                        on:click={() => {chs(time)}}
                    >I want this one!</button>
            </div>
        {/each}
    </div>
</main>