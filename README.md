<html>
    <head>
        <title>Corona App</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
        <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.16.0/umd/popper.min.js"></script>
        <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
        <link rel="stylesheet" href="./css/style.css">
    </head>
    <body>
        <h1>Covid19 Tracker</h1>
        <div>
        <form>
            <label>Enter country:</label> &nbsp;&nbsp;&nbsp;&nbsp;
            <input type="text" id="cname" placeholder="Enter country....">
            <br/><br/>
            <label>Enter start date:</label>&nbsp;
            <input type="date" id="sdate" placeholder="Start date..">
            <br/><br/>
            
            <label>Enter end date:</label>&nbsp;&nbsp;&nbsp;
            <input type="date" id="edate" placeholder="End date.."> 
            <br/><br/>

            <button class="btn btn-success" onClick="showData()">Submit</button>
        </form>

        <div id="res">
            <h4>Confirmed Cases:<span id="confirmed"></span> </h4>
            <h4>Active Cases: <span id="active"></span></h4>
            <h4>Death Cases: <span id="deaths"></span> </h4>
        </div>
    </div>
        <script src="./js/script.js"></script>
    </body>
</html>
 {
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
    -ms-box-sizing: border-box;
    -o-box-sizing: border-box;
    box-sizing: border-box;
}
body
{
    background-image: url(../image/background.webp);
    background-size: cover;
    background-repeat: no-repeat;
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
}
h1
{
    text-align: center;
    font-weight: bold;
}
div
{
    width:50%;
    background-color: blanchedalmond;
    margin: 25px;
    padding: 5%;
    margin: auto;
}
label
{
    font-size: 30px;
    font-weight: bold;
}
#res
{
    background-color: white;
    display: none;
    width: 100%;
}
function showData()
{
    event.preventDefault();
    var country=document.getElementById("cname").value;
    var sDate=document.getElementById("sdate").value;
    var eDate=document.getElementById("edate").value;

    var confirmed=document.getElementById("confirmed");
    var active=document.getElementById("active");
    var deaths=document.getElementById("deaths");

    console.log(sDate);

    if(country=='' || sDate=='' || eDate=='')
    alert("enter the required field");

    else
    {
        var url="https://api.covid19api.com/country/"+country+"?from="+sDate+"T00:00:00Z&to="+eDate+"T00:00:00Z";

        fetch(url)
        .then((res) => res.json())
        .then((res) => {
            console.log(res);
            var length=res.length;
            var index=length-1;

            var c=res[index].Confirmed;
            var a=res[index].Active;
            var d=res[index].Deaths;

            confirmed.innerHTML=c;
            active.innerHTML=a;
            deaths.innerHTML=d;

            document.getElementById("res").style.display="block";
            
        })
    }
}
