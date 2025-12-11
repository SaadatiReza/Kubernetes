# Installing RedisInsight Secure via Helm

This guide explains how to install **RedisInsight Secure** using the Helm chart from ArtifactHub.

---

## 1. Add the Helm Repository

Add the RedisInsight Secure Helm repository:

```bash
helm repo add redisinsight-secure https://github.com/liranme/redisinsight-secure/raw/main/helm/charts
helm repo update
'''


## 2. Download Default values.yml

Download the default values file if you want to modify it before installation:
'''bash
helm show values redisinsight-secure > values.yml
'''