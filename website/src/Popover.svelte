
<script>

    let visible = false;
    function toggleVisibility(){
        visible = ! visible;
    }
</script>


<div class="popover">
    <button class="toggle-btn" on:click={toggleVisibility} >{visible ? "x" : "i" }</button>
    

    {#if visible}
        <div class="content"  >
            <h3>Image Sources</h3>
            <ul>
                <li><a href="https://www.vecteezy.com/free-vector/soda-can-vector-free">Soda Can Vector Free Vectors by Vecteezy</a></li>
                <li><a href="https://www.vecteezy.com/free-vector/decorative">Decorative Vectors by Vecteezy</a></li>
            </ul>

            <h3>Code</h3>
            <ul>
                <li><a href="https://github.com/giggity-hub/ice-tea-name-generator">Github Repo</a></li>
            </ul>
        </div>
    {/if}



</div>


<style>

    .toggle-btn{
        background: white;
        border-radius: 50px;
        color: black;
        width: 30px;
        height: 30px;
        font-weight: bold;
        font-size: 20px;
        /* position: absolute; */

    }

    .popover{
        position: fixed;
        top: 30px;
        left: 30px;
        z-index: 5000;
        max-width: 85vw;

        background: white;
        border-radius: 15px;
        box-shadow: 0px 0px 0px 3px black;
        transition: all 5s;
        background: white;


    }
    .content{
        padding: 20px;
        padding-top: 0;
    }

    
</style>
