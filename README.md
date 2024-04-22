# Upgrade PRs - Private Packages
## Publish - private deps releases
1. Dispatch private deps release information via API. Use **POST https://apidocs.snyk.io/experimental?version=2023-11-20~experimental#post-/groups/-group_id-/packages** to submit private package data.
```
POST https://{{API_ENDPOINT}}/rest/groups/{{GROUP_ID}}/packages?version=2023-11-20~experimental
{
    "data": {
        "type":"package",
        "attributes": {
            "name": "logger",
            "namespace":"snyk",
            "version": "2.0.1",
            "type": "maven",
            "published_date":"2022-03-15T06:42:15.341Z"
        }
    }
}
```
2. Fetch recommendeded version using **GET https://apidocs.snyk.io/?version=2024-02-26~experimental#get-/groups/-group_id-/packages** .
```curl
GET https://{{API_ENDPOINT}}/rest/groups/{{GROUP_ID}}/packages/recommended_version?version=2024-02-26%7Eexperimental&namespace=snyk&name=logger&type=maven&current_version=1.0.0&allow_major_version=true
{
    "jsonapi": {
        "version": "1.0"
    },
    "data": {
        "type": "package",
        "id": "purl:maven/snyk/logger@2.0.1",
        "attributes": {
            "name": "logger",
            "version": "2.0.1",
            "type": "maven",
            "namespace": "snyk",
            "published_date": "2022-03-15T06:42:15.341Z"
        },
        "versions_diff": 9
    },
    "links": {}
}
```
## Raise Automatic Upgrade PRs for Private Packages
Automatic Upgrade PRs are created on each **Recurring tests** for both, *private* and *open-source* packages

## Configuration

1. Enable/Disable
2. Maximum # of opened upgrade PRs
3. Ignored deps
4. Allow major upgrades
5. Receive private packages upgrades recommendation. Enable / disable upgrade PRs for private deps
