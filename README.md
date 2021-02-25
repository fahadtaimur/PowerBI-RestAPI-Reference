# PowerBI-RestAPI-Reference
Quick guide to making POST request in Power Query M language

````
let
    
    # load the file
    Source = Csv.Document(File.Contents("test.txt"),[Delimiter=",", Columns=80, QuoteStyle=QuoteStyle.None]),
    
    # promote headers
    table = Table.PromoteHeaders(Source, [PromoteAllScalars=true]),
    
    * add additional steps for cleaning data here if needed*
    
    # specify endpoint for POST request
    api_url = "https://api.com/prediction/endpoint",
    
    # convert table to json format
    body = Json.FromValue(table),
    
    # make the request
    Data = Web.Contents(api_url,[Content=(body),Headers=[#"Content-Type"="application/json"]]),
    
    # Return the content of json document - https://docs.microsoft.com/en-us/powerquery-m/json-document
    DataRecord = Json.Document(Data),
    
    # Assign to a variable
    result=DataRecord,
    
    # Get the prediction
    predictions = result[predictions] 
    
in
    predictions

````
