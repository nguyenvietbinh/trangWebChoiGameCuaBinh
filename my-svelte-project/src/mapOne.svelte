<script>
    let characterX, isDeath, characterY, hole1, hole2, data = {
        hole: [900, 200, 100, 100]
    }, currentlyMap
    import Character from "./character.svelte";
    import { count, mapData } from './store.js'
    count.subscribe(value => {
        currentlyMap = value
    })
    function handleData(event) {
        characterX = event.detail[0]
        characterY = event.detail[1]
        isDeath = event.detail[2]
    }
    function holeIsOpen() {
        if(characterX >= 190) {
            hole1.style.display = 'block'
        }
        if(characterX >= 800) {
            hole2.style.display = 'block'
        }
        requestAnimationFrame(holeIsOpen)
    }
    function holeIsClose() {
        if(isDeath) {
            hole1.style.display = 'none'
            hole2.style.display = 'none'
        }
        requestAnimationFrame(holeIsClose)
    }
    import { onMount } from "svelte";
    onMount(() => {
        hole1 = document.querySelector('.hole1')
        hole2 = document.querySelector('.hole2')
        requestAnimationFrame(holeIsOpen)
        requestAnimationFrame(holeIsClose)
    })
</script>

<div class="backGround">
    <div class="stage">
        <div class="hole1"></div>
        <div class="hole2"></div>
        {#if currentlyMap === 1}
            <Character on:sendData={handleData}/>
        {/if}
        
        <div class="page">1</div>
    </div>
</div>

<style>
    .backGround {
        display: block;
        height: 100%;
        width: 100%;
        background-color: rgb(90, 90, 90);
        position: absolute;
        top: 0px;
        left: 0px;
    }
    .stage {
        display: block;
        height: 400px;
        width: 1198px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        left: calc(50% - 600px);
        top: calc(50% - 300px);
    }
    .hole2 {
        display: none;
        width: 100px;
        height: 200px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        top: 400px;
        left: 900px;
    }
    .hole1 {
        display: none;
        width: 100px;
        height: 200px;
        background-color: rgb(180, 180, 180);
        position: absolute;
        top: 400px;
        left: 200px;
    }
    .page {
        display: block;
        font-size: 100px;
        position: absolute;
        margin-top: 0%;
        top: 0px;
        left: 0px;
    }
</style>