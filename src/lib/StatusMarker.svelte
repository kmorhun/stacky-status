<div>
    <h3>{props.systemName}</h3>
    <p><span class="cardLabel">Port:</span> {props.systemPort == 0 ? "Null" : props.systemPort}</p>
    <p><span class="cardLabel">Mode:</span> {props.mode}</p>
    <p><span class="cardLabel">URL:</span> <a href=props.url>{props.url}</a></p>
    <p><span class="cardLabel">Status:</span> <span class="status" style="color: {statusColor}">{systemStatus}</span></p>
</div>

<style>
    .status {
        font-weight: bold;
    }

    .cardLabel {
        font-weight: bold;
    }

    div {
        border: 1px solid black;
        padding: 25px;
        margin: 10px;
        border-radius: 10px;
    }
    
</style>

<script>
    import axios from 'axios';
    export let props =  {
        systemName: "Test System",
        systemPort: 3000,
        mode: "development", // or "production"
        url: "http://beta.stacky.social:3000/ping"
    };

    let systemStatus;

    let success = null;

    // generate a new random number every 5 seconds
    $: {    
        setInterval(() => {
            axios.get(props.url)
                .then((res) => {
                    if (res.status == 200) {
                        console.log(props.systemName + " is connected with status " + res.status + " :)")
                        success = true;
                    } else {
                        console.log(res.status + "for " + props.systemName)
                        console.log(props.systemName + " is not connected :(")
                        success = false;
                    }
                })
                .catch((res) => {
                    console.log("Error for " + props.systemName + ": " + res)
                    // console.log(res)
                    success = false;
                });
        }, 5000);
    }

    $: systemStatus = (success == null) ? "Loading..." : (success ? "Online :)" : "Offline :(");
    $: statusColor = (success == null) ? "Blue" : (success ? "Green" : "Red");;

  
</script>
