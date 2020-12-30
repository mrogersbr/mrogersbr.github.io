<!DOCTYPE html>
<html>
    <head>
        <title>ItauCard 2 YNAB CSV </title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <script src="//code.jquery.com/jquery-git2.min.js"></script>
    </head>
    <body>
        <textarea id="fatura-text" name="fatura" cols="80" rows="30" placeholder="Cole o texto da fatura aqui"></textarea>
        <textarea id="fatura-converted" name="fatura" cols="80" rows="30" placeholder="O CSV aparecerá aqui.."></textarea>
        <br />
        <div id="result"></div>
        <script>
            config = {};
            config.linePattern = "";
            config.newLine = "\n";
            config.commonHeaders = "Date,Payee,Value";            
            config.populateMatches = function(fatura){
                var regex = /(\d*\/\d*)\t(.*)\t(-?[1-9]\d{0,2}(\.\d{3})*,\d{2})/g;
                var match = null;
                $("#fatura-converted").append(config.commonHeaders);
                $("#fatura-converted").append(config.newLine)
                
                while((match = regex.exec(fatura)) !== null){
                    $("#fatura-converted").append(match[1] + ";" + match[2] + ";" + match[3]);                    
                    $("#fatura-converted").append(config.newLine);
                }
                
            };
            
            $("#fatura-text").change(function(event){
                $("#fatura-converted").html("");
                config.populateMatches($("#fatura-text").val());
            })
        </script>
    </body>
</html>
