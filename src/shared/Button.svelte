<script>
export let type ='primary';
export let flat= false;
export let inverse = false;
</script>

<button class={type} class:flat={flat} class:inverse={inverse} on:click>
<slot>
</slot>
</button>

<style>
button{
    border:0;
    cursor: pointer;
    border-radius: 6px;
    padding: 8px 12px;
    font-weight: bold;
    box-shadow: 1px 2px 3px rgba(0,0,0,0.2)
}
.flat{
    box-shadow: none;
}

.primary.inverse{
    color:red;
    background: white;
    border: 2px solid red;
}

.secondary.inverse{
    color: green;
    background: white;
    border: 2px solid green;
}
.primary{
    background: red;
    color: white;
}
.secondary
{
    background: green;
    color: white;
}

</style>
