# Cloud-One-Conformity-Webhook-to-Azure-Log-Analytics
Azure function to accept alerts from Trend Micro Conformity webhook communication channel and output the log files to Azure Log Analytics workspaces / Sentinel. While parsing the message, the function adds one additional `timestamp` field using the `%Y-%m-%d %H:%M:%S` format based on the `lastModifiedDate` field in the json body of the Conformity communications channel output for easy sorting within Log Analytics.

## Prereqs
1. Install AZ cli tools https://docs.microsoft.com/en-us/cli/azure/install-azure-cli
2. Install Azure Functions Core Tools from NPM: https://www.npmjs.com/package/azure-functions-core-tools
3. Clone/download this repo.
4. Open the Azure Log Analytics console and navigate to Agents Management and note down the `WorkspaceID` and `PrimaryKey` values.

## Steps
1. Log into Azure via your terminal using `az login` 
2. Open `local.settings.json` file and update the values for `azcustomerid` with your log analytics workspace id, `azsharedkey` with the primary key. Optionally change the log group name with `log_type` key and save the file.
3. Publish the functions using the following command: `func azure functionapp publish <functionname> --publish-local-settings`
4. Copy down the return function URL from the output and input this in the webhooks communication channel within Conformity. Notifications with now start flowing into the log analytics workspace under the `TMConformity-CL` log group (name may vary if you modified the log group name in the earlier step).

## Support

Official support from Trend Micro is not available. Individual contributors may be Trend Micro employees, but are not official support.