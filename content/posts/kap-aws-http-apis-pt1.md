---
title: "Using AWS HTTP APIs (Part 1)"
subtitle: "Experiments using the AWS CLI"
date: 2021-12-20T18:57:58Z
draft: true
tags: ["killer-app-prepper", "aws", "api-gateway", "rest"]
---

Some text with `code` and stuff.


```bash
#!/usr/bin/env bash

api_id=$1

# Make an array from JSON. Nice. From https://unix.stackexchange.com/a/177845
api_info=( $(aws apigatewayv2 get-api --api-id $api_id | jq -r '.ApiId,.ProtocolType,.Name') )
echo ${api_info[@]}
printf "ID: %s  Protocol: %s  Name: %s\n"  ${api_info[0]} ${api_info[1]} ${api_info[2]}

all_route_ids=( $(aws apigatewayv2 get-routes --api-id $api_id | jq -r '.Items[].RouteId') )
echo ${all_route_ids[@]}

all_integration_ids=( $(aws apigatewayv2 get-integrations --api-id $api_id | jq -r '.Items[].IntegrationId') )
echo ${all_integration_ids[@]}


printf "%s\n" "$(tput smul)hsgsffs$(tput rmul)"
# Took forever to figure out that -r is needed or jq will return a quoted string
# (which subsequent bash commands don't like).
# https://stackoverflow.com/a/60103131/227441
INTEGRATION_IDS=$(aws apigatewayv2 get-integrations --api-id $API_ID | jq -r '.Items[].IntegrationId')
printf "$(tput bold)Integration Id$(tput sgr0): %s\n" $INTEGRATION_IDS

aws apigatewayv2 get-integration --api-id $API_ID --integration-id $INTEGRATION_IDS \
  | jq '.IntegrationId,.IntegrationMethod,.IntegrationType,.IntegrationUri'

printf "$(tput setaf 4)%s$(tput sgr0)\n" "color"
```

<!--more-->

 Test.

 That's some text with a footnote.[^1]

[^1]: And that's the footnote.