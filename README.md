# Data-Loss-Protection-PDF-Converter-
Sistema per anonimizzare i pdf che vengono caricati su un bucket 

This solution enables the automatic anonymization of sensitive data in PDF files using serverless Google Cloud services.

The process works as follows:
1. The file(s) is uploaded to an input bucket.
2. Once uploaded, it triggers a Cloud Function that invokes an API running on Cloud Run.
3. The Cloud Run API performs the following tasks:
   3.1 Splits the PDF into individual images, one per page.
   3.2 Calls the DLP API for each image to remove sensitive information.
   3.3 Merges the redacted images into a single PDF and uploads it to an output bucket.
   3.4 Stores the findings in BigQuery.

Mi sono inspirato al seguente progetto: https://github.com/GoogleCloudPlatform/dlp-pdf-redaction   
Per farlo funzionare ho dovuto apportare alcune modifiche, in particolare ai file 
- workflow-trigger.tf
- dlp-runner.tf

In questi file mancava la creazione del service-account e quindi ho aggiunto questi elementi nel tf (resource).


## Solution Architecture Diagram
![Solution Architecture Diagram]([percorso/dell/immagine.estensione](https://github.com/Maurodipa/Data-Loss-Protection-PDF-Converter-/blob/main/architecture-diagram.png))
