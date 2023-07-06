<script>
    export let cx = 0, cy = 0, r, a, text

    let x = cx + Math.sin(a * 2 * Math.PI / 360.0) * r
    let y = cy + Math.cos(a * 2 * Math.PI / 360.0) * r
</script>

<g transform={`translate(${x},${y}) rotate(${180 - a})`}>
    <text x={0} y={0} text-anchor="middle">
        {text}
    </text>
    <!-- 5개 최대 12자 -->
            <!-- 7개 최대 8자 -->
            <!-- 그 이상 4자 -->
</g>

<style>
    text {
        font-size: 24px;
        font-family: sans-serif;
        transform: rotate(90deg);
        /* transform-origin: 0, -12px; */
        /* transform-origin: center;
        position: relative; */
        fill: red;
    }
</style>