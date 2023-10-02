# synapse-demo

1. Deploy the infrastructure
    - IaC
    - Simple case:
      - 3 RGs for dev, test and prod
      - 3 Synapse analytics workspaces, one for each environment
      - data lake (1 or 3, what's the pattern?)
      - 3 key vault instances, one per environment
    - (Potential for a more complex scenario?)

2. Connect the only dev synapse workspace with your git repository (create one on ADO)
    - Depending on your project structure, you may choose to create a folder in the repo with all Synapse files or keep a different repository for that, isolating it from IaC, and others
    - Check the field to deploy existing resources and make sure that your repo target is empty to avoid conflicts
    - Keep the default collaboration and publishing branches
  
3. Add the `template-parameters-definition.json` from [this link](https://learn.microsoft.com/en-us/azure/synapse-analytics/cicd/continuous-integration-delivery#create-custom-parameters-in-the-workspace-template)
    - Best practice is to only expose those parameters that you want to work with for security reasons
    - Save the file in the main branch at the root of your Synapse workspace collaboration files with that exact name
  
4. Create the ADO pipeline:
    - Release pipeline (classic)
       - Create an empty release pipeline
       - For artifacts, point it at the Synapse publishing branch and get the ARM template and its parameters file
       - Stage 1 is deployment to test environment
           - Add the Synapse deployment task from the ADO marketplace
           - Complete the data and add the service principal; click on manage and follow the link to azure to get the SP name, and add it to the test RG (contributor RBAC) and to the Syanpse test Studio (Publisher RBAC)
           - Add relevant secrets to the test env key vault and connect it to the library
   
    
