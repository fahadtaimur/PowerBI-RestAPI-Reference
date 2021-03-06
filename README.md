# PowerBI-RestAPI-Reference
Quick guide to making POST request in Power Query M language

````
let
    
    # load the file
    source = Csv.Document(File.Contents("directory/predict.txt"), [Delimiter=",", Columns=number, QuoteStyle=QuoteStyle.None]),
    
    # promote headers
    table = Table.PromoteHeaders(source, [PromoteAllScalars=true]),
    
    *** add additional steps for cleaning data here if needed ***
    
    # specify endpoint for POST request
    api_url = "https://api.com/prediction/endpoint",
    
    # convert table to json format
    body = Json.FromValue(table),
    
    # make the request (non-token request)
    Data = Web.Contents(api_url, [Content=(body), Headers=[#"Content-Type"="application/json"]]),
    
    # Return the content of json document - https://docs.microsoft.com/en-us/powerquery-m/json-document
    DataRecord = Json.Document(Data),
    
    # Assign to a variable
    result=DataRecord,
    
    # Get the prediction
    predictions = result[predictions] 
    
in
    predictions

````
