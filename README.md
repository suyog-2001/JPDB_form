# JPDB_form

Description
I have created a form where a user can assign their Employee Id, Employee Name and their corresponding E-mail Address to the database. Where I have created one HTML file and attached javascript to it.

Benifits of JsonPowerDB
1. JsonPowerDB is a Deeloper Friendly API srvices.<br>
   2. JsonPowerDB is Light Weight, High Performance.<br>
   3. JsonPowerDB is Simple To use.<br>
   4. JsonPowerDB is Human Readable.<br>
   5. JsonPowerDB is Easy and fast to develop database applications without using any server side programming.

  
  
This JPDB Code that I have written to make this form :
    
     
        
        function createPUTRequest(connToken, jsonObj, dbName, relName) {
            var putRequest = "{\n"
                + "\"token\" : \""
                + connToken
                + "\","
                + "\"dbName\": \""
                + dbName
                + "\",\n" + "\"cmd\" : \"PUT\",\n"
                + "\"rel\" : \""
                + relName + "\","
                + "\"jsonStr\": \n"
                + jsonObj
                + "\n"
                + "}";
            return putRequest;
        }
        function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
            var url = dbBaseUrl + apiEndPointUrl;
            var jsonObj;
            $.post(url, reqString, function (result) {
                jsonObj = JSON.parse(result);
            }).fail(function (result) {
                var dataJsonObj = result.responseText;
                jsonObj = JSON.parse(dataJsonObj);
            });
            return jsonObj;
        }
        function resetForm() {
            $("#empId").val("")
            $("#empName").val("");
            $("#empEmail").val("");
            $("#empId").focus();
        }
        function saveEmployee() {
            var jsonStr = validateAndGetFormData();
            if (jsonStr === "") {
                return;
            }
            var putReqStr = createPUTRequest("90936861|-31948784479254024|90932362",
                jsonStr, "SAMPLE", "EMP-REL");
            alert(putReqStr);
            jQuery.ajaxSetup({ async: false });
            var resultObj = executeCommand(putReqStr,
                "http://api.login2explore.com:5577", "/api/iml");
            alert(JSON.stringify(resultObj));
            jQuery.ajaxSetup({ async: true });
            resetForm();
        }
    
</body>

</html>
![Screenshot (25)](https://user-images.githubusercontent.com/99820948/197394434-52534727-4e8a-45fc-96c6-76fb7839d47f.png)
