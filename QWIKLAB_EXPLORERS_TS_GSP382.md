# Mitigate Threats and Vulnerabilities with Security Command Center: Challenge Lab || [GSP382](https://www.cloudskillsboost.google/focuses/71935?parent=catalog) ||

# # Like, comment, share & Don't forget to subscribe [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN) 👍😄🤝

### Run the following Commands in CloudShell

```
gcloud scc muteconfigs create muting-flow-log-findings \
  --project=$DEVSHELL_PROJECT_ID \
  --location=global \
  --description="Rule for muting VPC Flow Logs" \
  --filter="category=\"FLOW_LOGS_DISABLED\"" \
  --type=STATIC

gcloud scc muteconfigs create muting-audit-logging-findings \
  --project=$DEVSHELL_PROJECT_ID \
  --location=global \
  --description="Rule for muting audit logs" \
  --filter="category=\"AUDIT_LOGGING_DISABLED\"" \
  --type=STATIC

gcloud scc muteconfigs create muting-admin-sa-findings \
  --project=$DEVSHELL_PROJECT_ID \
  --location=global \
  --description="Rule for muting admin service account findings" \
  --filter="category=\"ADMIN_SERVICE_ACCOUNT\"" \
  --type=STATIC

echo "${YELLOW}${BOLD}Check Score ${RESET}""${WHITE}${BOLD}for task 2${RESET}" "${GREEN}${BOLD}then press Y${RESET}"

# Delete the existing rule
gcloud compute firewall-rules delete default-allow-rdp

# Create a new rule with the updated source IP range
gcloud compute firewall-rules create default-allow-rdp \
  --source-ranges=35.235.240.0/20 \
  --allow=tcp:3389 \
  --description="Allow HTTP traffic from 35.235.240.0/20" \
  --priority=65534

# Delete the existing rule
gcloud compute firewall-rules delete default-allow-ssh --quiet

# Create a new rule with the updated source IP range
gcloud compute firewall-rules create default-allow-ssh \
  --source-ranges=35.235.240.0/20 \
  --allow=tcp:22 \
  --description="Allow HTTP traffic from 35.235.240.0/20" \
  --priority=65534

export ZONE=$(gcloud compute project-info describe \
--format="value(commonInstanceMetadata.items[google-compute-default-zone])")

echo "${CYAN}${BOLD}Click here: "${RESET}""${BLUE}${BOLD}""https://console.cloud.google.com/compute/instancesEdit/zones/$ZONE/instances/cls-vm?project=$DEVSHELL_PROJECT_ID"""${RESET}"
```

* **Reserve Static External IP** address name :
```
static-ip
```

### Run again the following Commands in CloudShell

```
export ZONE=$(gcloud compute project-info describe \
--format="value(commonInstanceMetadata.items[google-compute-default-zone])")

export REGION=$(echo "$ZONE" | cut -d '-' -f 1-2)

export VM_EXT_IP=$(gcloud compute instances describe cls-vm --zone=$ZONE \
  --format='get(networkInterfaces[0].accessConfigs[0].natIP)')

gsutil mb -p $DEVSHELL_PROJECT_ID -c STANDARD -l $REGION -b on gs://scc-export-bucket-$DEVSHELL_PROJECT_ID

gsutil uniformbucketlevelaccess set off gs://scc-export-bucket-$DEVSHELL_PROJECT_ID

curl -LO raw.githubusercontent.com/Titash-shil/Mitigate-Threats-and-Vulnerabilities-with-Security-Command-Center-Challenge-Lab-GSP382/refs/heads/main/QWIKLAB_EXPLORERS_GSP382_findings.jsonl

gsutil cp findings.jsonl gs://scc-export-bucket-$DEVSHELL_PROJECT_ID

echo "${CYAN}${BOLD}Click here: "${RESET}""${GREEN}${BOLD}""https://console.cloud.google.com/security/web-scanner/scanConfigs/edit?project=$DEVSHELL_PROJECT_ID"""${RESET}"

echo "${GREEN}${BOLD}Copy this: "${RESET}""${YELLOW}${BOLD}""http://$VM_EXT_IP:8080"""${RESET}"
```

# Congratulations ..!!🎉  You completed the lab shortly..😃💯

# *Well done..!* 👏

# Thank you for visiting.... :) 🗯️

# [Qwiklab_Explorers_ts](https://youtube.com/@titashshil?si=RgamNu1dc9jVIbJN)
