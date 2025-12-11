#https://artifacthub.io/packages/helm/redisinsight-secure/redisinsight-secure

Firstly the helm chart repository should be added to your helm repositories.

'''bash
helm repo add redisinsight-secure https://github.com/liranme/redisinsight-secure/raw/main/helm/charts
helm repo update
'''
Then download the default "values.yml" in case of any modification.
'''bash
helm show values redisinsight-secure > values.yml
'''

necessary parameters to be changed before installation

config.databaseManagement: true #Enable/disable database connection management
persistence.enabled: true #Enable persistent storage for RedisInsight data
ingress.enabled: true #Enable ingress resource for RedisInsight
ingress.basicauth.enabled #Enable HTTP basic authentication
ingress.basicauth.users #Configure a username and password to allow user login.

