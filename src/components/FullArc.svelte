<script>
    export let cx=0, cy=0, r


    let arcSweep = 1;

    let d = `
        M ${cx + r} ${cy}
        A ${r} ${r} 0 ${arcSweep} 0 ${cx - r} ${cy}
        A ${r} ${r} 0 ${arcSweep} 0 ${cx + r} ${cy}
    `;
</script>

<path {d}/>

<style>
    path {
        fill: green;
        stroke-width: 2;
        stroke: #fff;
    }
</style>
