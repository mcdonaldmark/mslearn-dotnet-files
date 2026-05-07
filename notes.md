# Web API Evidence

## Existing Records

- Pizza: Cheese Pizza
- Pizza: Pepperoni Pizza

## Added Record

- Pizza: Hawaiian Pizza

## Example API Test

GET /pizza  
Status: 200 OK  
Response:

[
{ "id": 1, "name": "Cheese Pizza" },
{ "id": 2, "name": "Pepperoni Pizza" },
{ "id": 3, "name": "Hawaiian Pizza" }
]

# Sales Summary

```csharp
void CreateSalesReport(IEnumerable<string> salesFiles, double total)
{
    var report = new StringBuilder();

    report.AppendLine("Sales Summary");
    report.AppendLine("----------------------------");
    report.AppendLine($"Total Sales: {total.ToString("C")}");
    report.AppendLine();
    report.AppendLine("Details:");

    foreach (var file in salesFiles)
    {
        string json = File.ReadAllText(file);
        SalesData? data = JsonConvert.DeserializeObject<SalesData?>(json);

        string relativePath = Path.GetRelativePath(storesDirectory, file);
        double fileTotal = data?.Total ?? 0;

        report.AppendLine($"  {relativePath}: {fileTotal.ToString("C")}");
    }

    var reportPath = Path.Combine(salesTotalDir, "salesReport.txt");
    File.WriteAllText(reportPath, report.ToString());
}
```
